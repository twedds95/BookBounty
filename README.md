# BookBounty

![Build Status](https://github.com/TheWicklowWolf/BookBounty/actions/workflows/main.yml/badge.svg)
![Docker Pulls](https://img.shields.io/docker/pulls/thewicklowwolf/bookbounty.svg)

<img src="/src/static/bookbounty.png" alt="image">


Web GUI for finding missing Readarr books.


## Run using docker-compose

```yaml
services:
  bookbounty:
    image: thewicklowwolf/bookbounty:latest
    container_name: bookbounty
    ports:
      - 5000:5000
    volumes:
      - /path/to/config:/bookbounty/config
      - /path/to/downloads:/bookbounty/downloads
      - /etc/localtime:/etc/localtime:ro
    restart: unless-stopped

```
---

## Configuration via environment variables

Certain values can be set via environment variables:

* __readarr_address__: The URL for Readarr. Defaults to `http://192.168.1.2:8787`.
* __readarr_api_key__: The API key for Readarr. Defaults to ` `.
* __libgen_address__: The URL for Library Genesis. Defaults to `http://libgen.is`.
* __sleep_interval__: Interval to sleep between downloads (seconds). Defaults to `0`.
* __sync_schedule__: Schedule times to run (comma seperated values in 24hr). Defaults to ` `.
* __minimum_match_ratio__: Minimum percentage for a match. Defaults to `90`.
* __selected_path_type__: Select Download Structure (file or folder). Defaults to `file`.
* __search_type__: Select Search Type (fiction or non-fiction). Defaults to `fiction`.
* __library_scan_on_completion__: Whether to scan Readarr Library on completion. Defaults to `True`.
* __request_timeout__: Timeout for requests (seconds). Defaults to `120`.
* __thread_limit__: Max number of threads to use. Defaults to `1`.
* __selected_language__: Filter download by language (specific languange or all). Defaults to `English`.
* __preferred_extensions_fiction__: Filter fiction download by extension (comma separated). Defaults to `.epub, .mobi, .azw3, .djvu`.
* __preferred_extensions_non_fiction__: Filter non-fiction download by extension (comma separated). Defaults to `.pdf .epub, .mobi, .azw3, .djvu`.


## Readarr Integration

You have two choices to integrate BookBounty with Readarr:

1. Directly map `/bookbounty/downloads` to your main Readarr folder and configure `selected_path_type=folder`.   
   This method will attempt to create the correct folder structure (`/author/book` etc.) and downloads files directly into their respective folders.

2. Alternatively, map `/bookbounty/downloads` to an `_unprocessed` folder and set `selected_path_type=file`.
   This method downloads all files into a single folder. After a library scan in Readarr, some files may remain unmapped and require manual import.
   You can use Readarr's "rename files" function to organize them into the correct folders after importing..

For both methods, setting `library_scan_on_completion=True` automates the import process in Readarr.

**Note:** Readarr does not automatically rename files upon import.


---


<img src="/src/static/dark.png" alt="image">


---


<img src="/src/static/light.png" alt="image">


---

https://hub.docker.com/r/thewicklowwolf/bookbounty

