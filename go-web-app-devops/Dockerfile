# Use the specific Go version from the official Go image
FROM golang:1.23 as base

# Set the working directory in the container
WORKDIR /app

# Copy the go.mod and go.sum files first
COPY go.mod ./

# Download dependencies. Dependencies will be cached if the go.mod and go.sum files are not changed
RUN go mod download

# Copy the source code into the container
COPY . .

# Build the Go app
RUN go build -o main1 .

FROM gcr.io/distroless/base

COPY --from=base /app/main1 .

COPY --from=base /app/static ./static

# Expose port 8080 to the outside world
EXPOSE 8080

# Run the executable
CMD ["./main1"]

