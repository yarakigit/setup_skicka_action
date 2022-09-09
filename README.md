# setup_skicka_action
---
## Setup for using skicka with GitHubActions
- [GitHub, google/skicka](https://github.com/google/skicka)

## GitHubActions Setup
1. Creating encrypted secrets for a repository
    - `GOOGLE_APIKEY` : `Google Cloud API Key`
    - `GOOGLE_CLIENT_SECRET` : `OAuth 2.0 Client Secret`
    - `SKICKA_TOKENCACHE_JSON` : `.skicka.tokencache.json` (Get by your Local Machine)
        - Copy to clipboard
            - Linux
            ~~~bash
            $ cat ~/.skicka.tokencache.json | xsel -bi
            ~~~
            - Mac
            ~~~bash
            $ cat ~/.skicka.tokencache.json | pbcopy
            ~~~
2. How to use this action
~~~yaml
name: 'Sample'

on:
  push:
    branches:
      - main
  workflow_dispatch:

jobs:
  setup-skicka:
    runs-on: ubuntu-latest 
    env:
      SKICKA_TOKENCACHE_JSON: ${{ secrets.SKICKA_TOKENCACHE_JSON }}      
      GOOGLE_CLIENT_SECRET: ${{ secrets.GOOGLE_CLIENT_SECRET }}
      GOOGLE_APIKEY: ${{ secrets.GOOGLE_APIKEY }}      
    steps: 
      - uses: yarakigit/setup_skicka_action@main
        with:
          SKICKA_TOKENCACHE_JSON: ${{ env.SKICKA_TOKENCACHE_JSON }}      
          GOOGLE_CLIENT_SECRET: ${{ env.GOOGLE_CLIENT_SECRET }}
          GOOGLE_APIKEY: ${{ env.GOOGLE_APIKEY }}
      - name: 'skicka sample'
        run: |
          skicka ls
~~~