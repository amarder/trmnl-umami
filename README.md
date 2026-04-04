# Umami TRMNL

![Graph with web pageview data and total pageviews and visitors at the top](screen.png)

A TRMNL plugin for [Umami Analytics](https://umami.is).

## Installation

### Via Recipe Fork

1. Go to the [Umami TRMNL Recipe](https://usetrmnl.com/recipes/25370/install)
2. Fork the recipe to your account (top right)

### Import

1. Download the [latest release](https://github.com/nicell/trmnl-umami/releases)'s plugin.zip file
2. Go to your [TRMNL plugin page](https://usetrmnl.com/plugins)
3. Connect Private Plugin if you haven't already
4. Go to [Private Plugin](https://usetrmnl.com/plugin_settings?keyname=private_plugin) from Connected list
5. Click Import new (top right)
6. Select the downloaded ZIP file

## Known Issues

### Only the full layout is working

The `half_horizontal`, `half_vertical`, and `quadrant` layouts are present but currently broken. Only `full` is actively developed and tested.



### Timezone in `.trmnlp.yml`

The top-level `time_zone` field in `.trmnlp.yml` is hardcoded rather than pulled from `UMAMI_TIMEZONE`. Ideally it would use `{{ env.UMAMI_TIMEZONE | default: 'America/New_York' }}` like the `custom_fields` entry does, but doing so breaks the dev preview. Until this is resolved upstream, update the hardcoded value in `.trmnlp.yml` manually if you need a different timezone.

## Local Development

Uses [trmnlp](https://github.com/usetrmnl/trmnlp) for a live-reloading preview without the zip/upload cycle.

### Prerequisites

Copy `.env.example` to `.env` and fill in your Umami credentials:

```bash
cp .env.example .env
```

See `.env.example` for details on each variable.

### Workflow

1. Open the project in Cursor and run **Dev Containers: Reopen in Container** from the command palette
2. In the container terminal, load your environment variables:
   ```bash
   set -a && source .env && set +a
   ```
3. Start the preview server:
   ```bash
   trmnlp serve
   ```
4. Port 4567 opens automatically in your browser — all four layout sizes are rendered side by side
5. Edit any file in `src/` and the preview reloads instantly

## Configuration

1. Set your preferred lookback period and time zone
2. Set your Umami instance hostname, API prefix, and website UUID

   **Self-hosted Umami:**
   - Hostname: `umami.example.com`
   - API Prefix: `api`
   - Website UUID: from the URL `https://umami.example.com/websites/<uuid>`

   **Umami Cloud:**
   - Hostname: `api.umami.is`
   - API Prefix: `v1`
   - Website UUID: from the URL `https://app.umami.is/websites/<uuid>`

3. Set your API key
   1.  Create a new user with only read access to the website you want to monitor
   2.  Create an API key for that user
       1.  [Self-hosted guide](https://umami.is/docs/api/authentication)
       2.  [Umami Cloud guide](https://umami.is/docs/cloud/api-key)
   3.  Copy the API key and paste it into the plugin configuration
