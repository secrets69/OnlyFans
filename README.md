# OnlyFans DataScraper (Python 3.9.X)

# ![app-token](examples/64255399-96a86700-cf21-11e9-8c62-87a483f33701.png)

# Mandatory Tutorial

Read the [#FAQ](README.md#faq) at the bottom of this page before submitting a issue.

## Running the app via docker

Build and run the image, mounting the appropriate directories:

`docker build -t only-fans . && docker run -it --rm --name onlyfans -v ${PWD}/.settings:/usr/src/app/.settings -v ${PWD}/.profiles:/usr/src/app/.profiles -v ${PWD}/.sites:/usr/src/app/.sites only-fans`

## Running on Linux

https://github.com/DIGITALCRIMINAL/OnlyFans/discussions/889

## Running the app locally

You need to install C++ Build Tools for the deephash module.

(I'll probably end up using something else since this is an annoying requirement)

https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2019

From the project folder open CMD/Terminal and run the command below:

`pip install -r requirements.txt`

Start:

`python start_ofd.py` or double click `start_ofd.py`

---

Open and edit:

`.profiles/default/auth.json`

[auth]

Fill in the following:

- `{"auth_id":"your_auth_id"}`
- `{"sess":"your_sess_token"}`
- `{"user-agent":"your_user-agent"}`

If you're using 2FA or have these cookies:

- `{"auth_hash":"your_auth_hash"}`
- `{"auth_uniq_":"your_auth_uniq_"}`

Optional change:

- `{"app-token":"your_token"}`

Only enter in cookies that reflect your OnlyFans account otherwise, you'll get auth errors.

Go to www.onlyfans.com and login, open the network debugger, then check the image below on how to get said above cookies

(Instead of typing "?app", type "api2")

![app-token](examples/1.png)

Your auth config should look similar to this

![app-token](examples/2.png)

If you get auth attempt errors, only YOU can fix it unless you're willing to let me into your account so I can see if it's working or not.
All issues about auth errors will be closed automatically. It's spam at this point, there's like 1000s of them and I don't care for anyone who can't use the search function lmao.

Note: If active is set to False, the script will ignore the profile.

# USAGE

`python start_ofd.py` or double click `start_ofd.py`

Enter in inputs as prompted by console.

# OPTIONAL

Open:

`config.json` (Open with a texteditor)

[settings]

### profile_directories:

Where your account information is stored (auth.json).

    Default = [".profiles"]

    If you're going to fill, please remember to use forward ("/") slashes only.

### download_directories:

Where downloaded content is stored.

    Default = [".sites"]

    If you're going to fill, please remember to use forward ("/") slashes only.

    You can add multiple directories and the script will automatically rollover to the next directory if the current is full.

### metadata_directories:

Where metadata content is stored.

    Default = [".sites"]

    If you're going to fill, please remember to use forward ("/") slashes only.

    Automatic rollover not supported yet.

### path_formatting:

Overview for [file_directory_format](#file_directory_format), [filename_format](#filename_format) and [metadata_directory_format](#metadata_directory_format)

    {site_name} = The site you're scraping.

    {first_letter} = First letter of the model you're scraping.

    {post_id} = The posts' ID.

    {media_id} = The media's ID.

    {username} = The account's username.

    {api_type} = Posts, Messages, etc.

    {media_type} = Images, Videos, etc.

    {filename} = The media's filename.

    {value} = Value of the content. Paid or Free.

    {text} = The media's text.

    {date} = The post's creation date.

    {ext} = The media's file extension.

    Don't use the text variable. If you do, enjoy emojis in your filepaths and errors lmao.

### file_directory_format:

This puts each media file into a folder.

The list below are unique identifiers that you must include.

You can choose one or more.

    Default = "{site_name}/{username}/{api_type}/{value}/{media_type}"
    Default Translated = "OnlyFans/belledelphine/Posts/Free/Images"

    {username} = belledelphine

### filename_format:

Usage: Format for a filename

The list below are unique identifiers that you must include.

You must choose one or more.

    Default = "{filename}.{ext}"
    Default Translated = "5fb5a5e4b4ce6c47ce2b4_source.mp4"

    {filename} = 5fb5a5e4b4ce6c47ce2b4_source
    {media_id} = 133742069

### metadata_directory_format:

Usage: Filepath for metadata. It's tied with download_directories so ignore metadata_directories in the config.

The list below are unique identifiers that you must include.

You must choose one or more.

    Default = "{site_name}/{username}/Metadata"
    Default Translated = "OnlyFans/belledelphine/Metadata"

    {username} = belledelphine

### text_length:

Usage: When you use {text} in filename_format, a limit of how many characters can be set by inputting a number.

    Default = ""
    Ideal = "50"
    Max = "255"

    The ideal is actually 0.

### video_quality:

Usage: Select the resolution of the video.

    Default = "source"
    720p = "720" | "720p"
    240p = "240" | "240p"

### auto_site_choice:

Usage: You can automatically choose which site you want to scrape.

    Default = ""

    OnlyFans = "onlyfans"

### auto_choice:

Usage: You can automatically choose which media type you want to scrape.
Default = ""

    Everything = "a"
    Images = "b"
    Videos = "c"
    Audios = "d"

    You can automatically choose which type of media you want to scrape.

### auto_scrape_names:

    Default = false

    If set to true, the script will scrape all the names.

### auto_scrape_apis:

    Default = true

    If set to false, you'll be given the option to scrape individual apis.

### jobs:

    "scrape_names" - This will scrape your standard content
    "scrape_paid_content" - This will scrape paid content

    If set to false, it won't do the job.

### export_type:

    Default = "json"

    JSON = "json"

    You can export an archive to different formats (not anymore lol).

### overwrite_files:

    Default = false

    If set to true, any file with the same name will be redownloaded.

### date_format:

    Default = "%d-%m-%Y"

    If you live in the USA and you want to use the incorrect format, use the following:

    "%m-%d-%Y"

### max_threads:

    Default = -1

    When number is set below 1, it will use all threads.
    Set a number higher than 0 to limit threads.

### min_drive_space:

    Default = 0
    Type: Float

    Space is calculated in GBs.
    0.5 is 500mb, 1 is 1gb,etc.
    When a drive goes below minimum drive space, it will move onto the next drive or go into an infinite loop until drive is above the minimum space.

### webhooks:

    Default = []

    Supported webhooks:
    Discord

    Data is sent whenever you've completely downloaded a model.
    You can also put in your own custom url and parse the data.
    Need another webhook? Open an issue.

### exit_on_completion:

    Default = false

    If set to true the scraper run once and exit upon completion, otherwise the scraper will give the option to run again. This is useful if the scraper is being executed by a cron job or another script.

### infinite_loop:

    Default = true

    If set to false, the script will run once and ask you to input anything to continue.

### loop_timeout:

    Default = 0

    When infinite_loop is set to true this will set the time in seconds to pause the loop in between runs.

### boards:

    Default = []
    Example = ["s", "gif"]

    Input boards names that you want to automatically scrape.

### ignored_keywords:

    Default = []
    Example = ["ignore", "me"]

    Any words you input, the script will ignore any content that contains these words.

### ignore_type:

    Default = ""
    a = "paid"
    b = "free"

    This setting will not include any paid or free accounts in your subscription list.

    Example: "ignore_type": "paid"

    This choice will not include any accounts that you've paid for.

### export_metadata:

    Default = true

    Set to false if you don't want to save metadata.

### blacklist_name:

    Default = ""

    This setting will not include any blacklisted usernames when you choose the "scrape all" option.

    Go to https://onlyfans.com/my/lists and create a new list; you can name it whatever you want but I called mine "Blacklisted".

    Add the list's name to the config.

    Example: "blacklist_name": "Blacklisted"

    You can create as many lists as you want.

# FAQ

Before troubleshooting, make sure you're using Python 3.9.

Error: Access Denied / Auth Loop

> Make sure your cookies and user-agent are correct.
> Use this tool [Cookie Helper](https://github.com/M-rcus/OnlyFans-Cookie-Helper)

AttributeError: type object 'datetime.datetime' has no attribute 'fromisoformat'

> Only works with Python 3.7 and above.

I can't see ".settings" folder'

> Make sure you can see hidden files
>
> [Windows Tutorial](https://support.microsoft.com/en-gb/help/4028316/windows-view-hidden-files-and-folders-in-windows-10)
>
> [Mac Tutorial](https://setapp.com/how-to/show-hidden-files-on-mac)
>
> [Linux](https://www.google.com)

I'm getting authed into the wrong account

> Enjoy the free content. | This has been patched lol.

I'm using Linux OS and something isn't working.

> Script was built on Windows 10. If you're using Linux you can still submit an issue and I'll try my best to fix it.

Am I able to bypass paywalls with this script?

> Hell yeah! My open source script can bypass paywalls for free.
> [Tutorial](https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcS5hTXe02DNlsktpFfkrr--OQ0ScILMibxmpQ&usqp=CAU)

Do OnlyFans or OnlyFans models know I'm using this script?

> No, but there is identifiable information in the metadata folder which contains your IP address, so don't share it unless you're using a proxy/vpn or just don't care.

Do you collect session information?

> No. The code is on Github which allows you to audit the codebase yourself. You can use wireshark or any other network analysis program to verify the outgoing connections are respective to the modules you chose.

Does this script violate the Onlyfans.com ToS?

> No...
> OnlyFans themselves allow users to download content as stated in their [Terms of Service](https://onlyfans.com/terms)

> 8.2.2 you may print or download one copy of a reasonable number of pages of the Website for your own personal, non-commercial use and not for further reproduction, publication, or distribution."

Disclaimer:

> OnlyFans is a registered trademark of Fenix International Limited.

> The contributors of this script isn't in any way affiliated with, sponsored by, or endorsed by Fenix International Limited.

> The contributors of this script are not responsible for the end users' actions.

> LMAO
