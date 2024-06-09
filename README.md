git clone ssh://codeserver.dev.simonarmin@codeserver.dev.simonarmin.drush.in:2222/~/repository.git armin-cpa
cd armin-cpa
git remote add github https://github.com/armincpa/armin-cpa.git
git push github main
mkdir -p .github/
name: Deploy to Pantheon

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2

    - name: Set up SSH
      uses: webfactory/ssh-agent@v0.5.3
      with:
        ssh-private-key: ${{ secrets.codeserver.dev.simonarmin@codeserver.dev.simonarmin.drush.in:2222/~/repository.git armin-cpa}}

    - name: Deploy to Pantheon
      run: |
        git remote add pantheon ssh://codeserver.dev.armincpa@codeserver.dev.armincpa.drush.in:2222/~/repository.git
        git push pantheon main
