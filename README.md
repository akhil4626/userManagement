name: User Management System
on:
push:
pull_request:
schedule:
- cron: "0 * * * *"

jobs:
build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Setup Node
        uses: actions/setup-node@v1
        with:
          node-version: "12.x"s
      - name: Install Dependencies
        run: npm install
      - name: Run app.js
        run: npm start
        env:
          AIRTABLE_API_KEY: ${{secrets.AIRTABLE_API_KEY}}
      - name: Commit the new README.MD file
        run: |-
          git diff
          git config --global user.email "your email"
          git config --global user.name "your name"
          git diff --quiet || (git add README.md && git commit -m "Update the README.md file")
          git push
