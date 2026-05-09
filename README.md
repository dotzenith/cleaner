# lc

A CLI tool that removes tracking parameters and junk from URLs. Based on [Link Cleaner](https://github.com/corbindavenport/link-cleaner) by Corbin Davenport.

## Build

```sh
git clone https://github.com/dotzenith/cleaner
cd cleaner
cargo build --release
```

The binary is at `target/release/lc`.

## Usage

```sh
lc [OPTIONS] <URL>
```

### Examples

```sh
# Basic cleaning
lc "https://example.com?utm_source=test"
# → https://example.com/

# Shorten YouTube links
lc "https://www.youtube.com/watch?v=dQw4w9WgXcQ" --youtube-short
# → https://youtu.be/dQw4w9WgXcQ

# Copy result to clipboard
lc "https://example.com?foo=bar" --clipboard

# Use a custom config file
lc "https://example.com" --config /path/to/config.toml
```

### Options

| Flag              | Description                                         |
|-------------------|-----------------------------------------------------|
| `--youtube-short` | Shorten YouTube video links to `youtu.be`           |
| `--walmart-short` | Shorten Walmart product links to `walmart.com/ip/{id}` |
| `--fix-twitter`   | Replace `twitter.com` / `x.com` with `fxtwitter.com` |
| `--fix-bluesky`   | Replace `bsky.app` with `fxbsky.app`                |
| `--amazon-tag <ID>` | Append Amazon affiliate tracking ID                 |
| `--clipboard`     | Copy the cleaned URL to the system clipboard        |
| `--verbose`       | Print old link, settings, new link to stderr        |
| `--config`        | Path to a custom configuration file                 |
| `--version`       | Print version                                       |
| `-h`, `--help`    | Print help                                          |

## Configuration

`lc` reads an optional config file at `~/.config/lc/config.toml`. CLI flags override config values.

### Example `config.toml`

```toml
youtube_shorten = true
walmart_shorten = true
fix_twitter = false
fix_bluesky = false
amazon_tracking_id = "mytag-20"
```

## License

GPL-3.0
