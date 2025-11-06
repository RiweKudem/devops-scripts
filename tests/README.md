#!/bin/bash

# Set script directory
SCRIPT_DIR=$(dirname "$(readlink -f "$0")")

# Set script name
SCRIPT_NAME=$(basename "$0")

# Print header
echo "DevOps Scripts"
echo "=============="

# Print usage
echo "Usage: $SCRIPT_NAME <command> [options]"
echo "Available commands:"
echo "  init  Initialize a new project"
echo "  build Build a project"
echo "  deploy Deploy a project"
echo "  clean Clean up project files"
echo "  help  Show this help message"

# Check if command is provided
if [ $# -eq 0 ]; then
  echo "Error: No command provided"
  exit 1
fi

# Check if command is valid
case $1 in
  init) init_project ;;
  build) build_project ;;
  deploy) deploy_project ;;
  clean) clean_project ;;
  help) print_help ;;
  *) echo "Error: Unknown command '$1'" >&2; exit 1 ;;
esac

# Define init_project function
init_project() {
  echo "Initializing a new project..."
  # Create project directory
  mkdir -p "$SCRIPT_DIR/../project"
  # Create project files
  echo "Creating project files..."
  touch "$SCRIPT_DIR/../project/.gitignore"
  touch "$SCRIPT_DIR/../project/.env"
  echo "Project initialized."
}

# Define build_project function
build_project() {
  echo "Building a project..."
  # Run build command
  echo "Building project..."
  # Run make command
  make
  echo "Project built."
}

# Define deploy_project function
deploy_project() {
  echo "Deploying a project..."
  # Run deploy command
  echo "Deploying project..."
  # Run rsync command
  rsync -avz "$SCRIPT_DIR/../project/" "$SCRIPT_DIR/../deploy/"
  echo "Project deployed."
}

# Define clean_project function
clean_project() {
  echo "Cleaning up project files..."
  # Remove project directory
  rm -rf "$SCRIPT_DIR/../project"
  echo "Project cleaned up."
}

# Define print_help function
print_help() {
  echo "Showing help message..."
  cat <<EOF
Usage: $SCRIPT_NAME <command> [options]

Available commands:
  init  Initialize a new project
  build Build a project
  deploy Deploy a project
  clean Clean up project files
  help  Show this help message
EOF
}

# Call main function
main "$@"