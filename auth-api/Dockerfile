# Use Go as base image
FROM golang:1.19-alpine AS build

# Set working directory
WORKDIR /app

# Copy go module files
COPY go.mod go.sum ./

# Download dependencies
RUN go mod download

# Copy source code
COPY . .

# Build the application
RUN CGO_ENABLED=0 GOOS=linux go build -o auth-api .

# Use a small alpine image for the final image
FROM alpine:3.17

# Copy the binary from the build stage
COPY --from=build /app/auth-api /usr/local/bin/

# Expose the port
EXPOSE 8000

# Run the binary
CMD ["auth-api"]
