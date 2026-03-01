# github actions yaml file:


name: GitHub Pages CI/CD

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    name: Build site
    runs-on: ubuntu-latest
    environment: dev

    steps:
      - uses: actions/checkout@v4

      - name: Build static site
        run: |
          mkdir dist
          echo "<h1>Hello GitHub Pages</h1>" > dist/index.html

      - name: Upload Pages artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: dist

  test:
    name: Promote to Test
    needs: build
    runs-on: ubuntu-latest
    environment: test

    steps:
      - name: Test gate
        run: echo "Test checks passed"

  deploy:
    name: Deploy to GitHub Pages
    needs: test
    runs-on: ubuntu-latest
    environment:
      name: prod
      url: ${{ steps.deployment.outputs.page_url }}

    steps:
      - name: Deploy
        id: deployment
        uses: actions/deploy-pages@v4
