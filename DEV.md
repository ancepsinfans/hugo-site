# Running Hugo Site Locally for Development

## Prerequisites

Install Hugo Extended (required for this theme). The site uses Hugo v0.95.0.

### Option 1: Install via package manager (Ubuntu/Debian)

```bash
# Download Hugo Extended
wget https://github.com/gohugoio/hugo/releases/download/v0.95.0/hugo_extended_0.95.0_Linux-64bit.deb

# Install
sudo dpkg -i hugo_extended_0.95.0_Linux-64bit.deb

# Verify installation
hugo version
```

### Option 2: Install via snap

```bash
sudo snap install hugo --channel=extended
```

### Option 3: Download binary directly

```bash
# Download Hugo Extended binary
wget https://github.com/gohugoio/hugo/releases/download/v0.95.0/hugo_extended_0.95.0_Linux-64bit.tar.gz

# Extract and move to PATH
tar -xzf hugo_extended_0.95.0_Linux-64bit.tar.gz
sudo mv hugo /usr/local/bin/
```

## Running the Development Server

Once Hugo is installed, navigate to the site directory and run:

```bash
cd /home/bullard/docker-services/hugo-site
hugo server
```

This will:
- Start a local development server (usually at `http://localhost:1313`)
- Watch for file changes and automatically reload
- Show draft content and future-dated posts

### Additional Options

- **Bind to all interfaces** (accessible from other devices on your network):
  ```bash
  hugo server --bind 0.0.0.0
  ```

- **Specify a different port**:
  ```bash
  hugo server --port 8080
  ```

- **Disable Fast Render Mode** (if you encounter issues):
  ```bash
  hugo server --noHTTPCache
  ```

- **Build for production** (like Netlify does):
  ```bash
  hugo --gc --minify
  ```

## Theme

The site uses the `toha` theme, which is included as a git submodule. If you need to update it:

```bash
git submodule update --init --recursive
```

## Troubleshooting

- If you get errors about missing images, ensure all image files exist in `assets/images/`
- If the theme doesn't load, make sure the submodule is initialized: `git submodule update --init --recursive`
- For production builds, use `hugo --gc --minify` as configured in `netlify.toml`
