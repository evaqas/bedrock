# [Bedrock](https://roots.io/bedrock/)

```bash
# create bedrock project
create-project() {
    local htdocs_dir="/Applications/MAMP/htdocs";

    if [ -z "$1" ]; then
        echo "No destination directory provided."
        return 0
    fi

    cd "${htdocs_dir}"
    git clone https://github.com/evaqas/bedrock "$1"
    cd "$1"
    git archive -o "../$1.zip" master
    cd ..
    rm -rf "$1"
    unzip "$1.zip" -d "$1"
    rm -f "$1.zip"
    cd "$1"
    cp .env.example .env
    cp .htaccess.example .htaccess
    composer install
}

# cd into bedrock theme dev dir
bedrockdir() {
    local htdocs_dir="/Applications/MAMP/htdocs";

    if [ -z "$1" ]; then
        cd "${htdocs_dir}"
    elif [ -d "${htdocs_dir}/$1" ]; then
        cd "${htdocs_dir}/$1/web/app/themes/dev"
    else
        echo "Directory not found: ${htdocs_dir}/$1"
    fi
}
```
