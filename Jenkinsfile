pipeline {
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v3
      
      - name: Build Docker Image
        run: docker build -t sophie14/api-tests:latest .
      
      - name: Push Docker Image to Docker Hub
        run: docker push sophie14/api-tests:latest
}