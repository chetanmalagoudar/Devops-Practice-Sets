###########################################
# BASE IMAGE
###########################################

FROM ubuntu AS build

RUN apt-get update && apt-get install -y golang-go

ENV GO111MODULE=off

COPY . .


RUN CGO_ENABLED=0 go build -o /app .

############################################
# HERE STARTS THE MAGIC OF MULTI STAGE BUILD
############################################

# Minimalistic distroless image that we have today
FROM scratch

# Copy the compiled binary from the build stage
COPY --from=build /app /app

# Set the entrypoint for the container to run the binary
ENTRYPOINT ["/app"]




## Why did we use scratch ??

# In the provided Dockerfile, we use the scratch base image for the final runtime stage.
#  The scratch image is a special minimal image provided by Docker, and it is often used for building distroless images, meaning images without any OS or libraries. 
#  Using scratch as the base image means we are starting with a completely empty slate, and we only add the specific files we need for our application.