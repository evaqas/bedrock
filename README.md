<p>
    <a href="https://roots.io/bedrock/">
        <img alt="Bedrock" src="https://cdn.roots.io/app/uploads/logo-bedrock.svg" height="100">
    </a>
</p>

## Setup
1. Add this function to ``~/.bash_profile``:
```bash
create-project() {
    local sites_dir="/Users/username/Local Sites"

    if [ -z "$1" ]; then
        echo "No destination directory provided."
        return 0
    fi

    cd "${sites_dir}/$1/app"
    git clone https://github.com/evaqas/bedrock "$1"
    cd "$1"
    git archive -o "../$1.zip" master
    cd ..
    rm -rf "$1"
    rm -rf public
    unzip "$1.zip"
    rm -f "$1.zip"
    mv .env.example .env
}
```
2. Create a project in Local by Flywheel. Click TRUST a certificate in SSL tab.
3. Run ``create-project project-name`` from terminal where ``project-name`` equals project name in Local.
4. Configure ``.env`` values.
5. Run ``composer install``.
6. Edit Apache config: ``code ../conf/apache/site.conf.hbs``.
   - Set DocumentRoot and &lt;Directory&gt; to ``/Users/username/Local Sites/project-name/app/public_html``.
   - Restart Local web server.
