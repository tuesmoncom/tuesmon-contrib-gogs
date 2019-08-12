> **NOTE:** This plugin is **DEPRECATED** since Tuesmon 3.0.0 (2016-10-02) because it was included in the core of Tuesmon.

Tuesmon contrib gogs
==================

![Kaleidos Project](http://kaleidos.net/static/img/badge.png "Kaleidos Project")
[![Managed with Tuesmon.com](https://tuesmon.com/media/support/attachments/article-22/banner-gh.png)](https://tuesmon.com "Managed with Tuesmon.com")

The Tuesmon plugin for gogs integration.

Installation
------------
### Production env

#### Tuesmon Back

In your Tuesmon back python virtualenv install the pip package `tuesmon-contrib-gogs` with:

```bash
  pip install tuesmon-contrib-gogs
```

Modify in `tuesmon-back` your `settings/local.py` and include the line:

```python
  INSTALLED_APPS += ["tuesmon_contrib_gogs"]
  PROJECT_MODULES_CONFIGURATORS["gogs"] = "tuesmon_contrib_gogs.services.get_or_generate_config"
```

The run the migrations to generate the new need table:

```bash
  python manage.py migrate tuesmon_contrib_gogs
```

#### Tuesmon Front

Download in your `dist/plugins/` directory of Tuesmon front the `tuesmon-contrib-gogs` compiled code (you need subversion in your system):

```bash
  cd dist/
  mkdir -p plugins
  cd plugins
  svn export "https://github.com/tuesmoncom/tuesmon-contrib-gogs/tags/$(pip show tuesmon-contrib-gogs | awk '/^Version: /{print $2}')/front/dist" "gogs"
```

Include in 'dist/conf.json' in the 'contribPlugins' list the value `"/plugins/gogs/gogs.json"`:

```json
...
    "contribPlugins": [
        (...)
        "/plugins/gogs/gogs.json"
    ]
...
```

### Dev env

#### Tuesmon Back

Clone the repo and

```bash
  cd tuesmon-contrib-gogs/back
  workon tuesmon
  pip install -e .
```

Modify in `tuesmon-back` your `settings/local.py` and include the line:

```python
  INSTALLED_APPS += ["tuesmon_contrib_gogs"]
  PROJECT_MODULES_CONFIGURATORS["gogs"] = "tuesmon_contrib_gogs.services.get_or_generate_config"
```

The run the migrations to generate the new need table:

```bash
  python manage.py migrate tuesmon_contrib_gogs
```

#### Tuesmon Front

After clone the repo link `dist` in `tuesmon-front` plugins directory:

```bash
  cd tuesmon-front/dist
  mkdir -p plugins
  cd plugins
  ln -s ../../../tuesmon-contrib-gogs/dist gogs
```

Include in 'dist/conf.json' in the 'contribPlugins' list the value `"/plugins/gogs/gogs.json"`:

```json
...
    "contribPlugins": [
        (...)
        "/plugins/gogs/gogs.json"
    ]
...
```

In the plugin source dir `tuesmon-contrib-gogs/front` run

```bash
npm install
```
and use:

- `gulp` to regenerate the source and watch for changes.
- `gulp build` to only regenerate the source.

