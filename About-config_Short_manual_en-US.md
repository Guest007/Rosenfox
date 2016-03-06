*(Sorry, English is not my native language)*

## I. CREATE NEW PROFILE

Use the Profile Manager to create new Firefox profile. 

LINUX:

    $ firefox -P

WINDOWS:

    "C:\Program Files\Mozilla Firefox\firefox.exe" -p

Or:

    "C:\Program Files (x86)\Mozilla Firefox\firefox.exe" -P

In the Profile Manager, click Create Profile... to start the Create Profile Wizard. Click Next and enter the name of the profile. To create the new profile, click Finish. 

If the Profile Manager window still does not open, Firefox may have been running in the background, even though it was not visible. Close all instances of Firefox or restart the computer and then try again.

https://support.mozilla.org/en-US/kb/profile-manager-create-and-remove-firefox-profiles


## II. OPEN PREFERENCES

After browser's start, type about:config in the Location Bar (address bar) and press Enter to display the list of preferences:

    about:config

http://kb.mozillazine.org/About:config


## III. CHANGE SETTINGS


- SCRIPTS

Block all JavaScript's elements. JavaScript is programming language; one of the main web-technologies. But JavaScript provides the potential to run dangerous scripts on a client computer. XSS vulnerabilities occur when an attacker is able to include a malicious script in the page presented to a user. The script can access to the site with the user's privileges. CSRF vulnerability: malicious code on an attacker's site force browser to taking undesirable actions on a target site (for example - transferring money). JavaScript can allow leaks of various information about OS, browser, monitor size/resolution, installed fonts, other data. 

JavaScript in content can not execute:

    javascript.enabled=false

http://kb.mozillazine.org/Javascript.enabled

JavaScript's additional settings (white-list):

You can create a JavaScript site "white-list". In user.js, add the following lines:

    user_pref("capability.policy.policynames", "jsok");
    user_pref("capability.policy.default.javascript.enabled", "noAccess");
    user_pref("capability.policy.jsok.sites", "http://www.safe-site-1.com  https://safe-site-2.net");
    user_pref("capability.policy.jsok.javascript.enabled", "allAccess");

http://kb.mozillazine.org/Allowing_only_certain_sites_to_use_JavaScript

**Attention:** Change "http://www.safe-site-1.com  https://safe-site-2.net" etc. to preferred links.


- DOM (Document Object Model) storage

The Web Applications specification defines a mechanism allowing web pages to store information with a web browser - client-side session and persistent storage. Switch to:

    dom.storage.enabled=false

http://kb.mozillazine.org/Dom.storage.enabled

https://en.wikipedia.org/wiki/Document_Object_Model

- DOM JavaScript

When a web page is loaded, the browser creates a Document Object Model of the page. To prevent probably not-secure or potentially dangerous actions:

a) JavaScript can add, change, and remove all the HTML elements and attributes in the page.

b) JavaScript can change all the CSS styles in the page.

c) JavaScript can react to all existing events in the page.

d) JavaScript can create new events in the page.

You must set:

    dom.allow_scripts_to_close_windows=false
    dom.disable_window_flip=true
    dom.disable_window_move_resize=true
    dom.disable_window_open_feature.close=true
    dom.disable_window_open_feature.location=true
    dom.disable_window_open_feature.menubar=true
    dom.disable_window_open_feature.minimizable=true
    dom.disable_window_open_feature.resizable=true
    dom.disable_window_open_feature.scrollbars=true
    dom.disable_window_open_feature.status=true
    dom.disable_window_open_feature.personalbar=true
    dom.disable_window_open_feature.titlebar=true
    dom.disable_window_open_feature.toolbar=true

We strongly recommend to disable other DOM's functions:

    browser.dom.window.dump.enabled=false
    dom.indexedDB.enabled=false
    dom.archivereader.enabled=false
    dom.cellbroadcast.enabled=false
    dom.event.clipboardevents.enabled=false
    dom.datastore.enabled=false
    dom.enable_performance=false
    dom.enable_resource_timing=false
    dom.fetch.enabled=false
    dom.gamepad.enabled=false
    dom.gamepad.non_standard_events.enabled=false
    dom.icc.enabled=false
    dom.identity.enabled=false
    dom.mobileconnection.enabled=false
    dom.mozAlarms.enabled=false
    dom.mozApps.used=false
    dom.mozContacts.enabled=false
    dom.mozNetworkStats.enabled=false
    dom.mozSettings.enabled=false
    dom.netinfo.enabled=false
    dom.sms.enabled=false
    dom.server-events.enabled=false
    dom.telephony.enabled=false
    dom.voicemail.enabled=false
    dom.wakelock.enabled=false
    dom.webcomponents.enabled=false
    dom.webnotifications.enabled=false


- COOKIES

Cookie is a small data (text file) sent from a server and stored in browser. Then the user loads the same webpage again, the browser sends the cookie back to the server and notify about previous activity. Cookies were designed to remember stateful information: passwords, logins, session data, credit card's data, e-mail and record browsing activity.

No cookies are allowed: 

    network.cookie.cookieBehavior=2 (recommended)

http://kb.mozillazine.org/Network.cookie.cookieBehavior

Only cookies from the originating server are allowed. Third-party cookies are disabled: 

    network.cookie.cookieBehavior=1 (not recommended)

**Attention:** If you want to use original cookies, set correct lifetime policy. The cookie expires at the end of the session (when the browser closes):

    network.cookie.lifetimePolicy=2

http://kb.mozillazine.org/Network.cookie.lifetimePolicy
 

- USER AGENT

User-Agent string (part oh HTTP-header) is often used for content negotiation, where the server selects suitable data or operating parameters for the response. UA string might be used by server to choose variants based on the known capabilities of a particular version of client software.

Create a fake (or empty) UA-string (create - string - text):

    general.useragent.override=[empty]

Or, for example:

    general.useragent.override="Mozilla/5.0 (Windows NT 6.1; rv:38.0) Gecko/20100101 Firefox/38.0"

Or, you can add expanded strings and settings, for example:

    general.appname.override", "Netscape"
    general.appversion.override", "5.0 (Windows)"
    general.oscpu.override", "Windows NT 6.1"
    general.platform.override", "Win32"
    general.useragent.override", "Mozilla/5.0 (Windows NT 6.1; rv:38.0) Gecko/20100101 Firefox/38.0"
    general.productSub.override", "20100101"
    general.buildID.override", "20100101"
    browser.startup.homepage_override.buildID", "20100101"

https://developer.mozilla.org/en-US/docs/Web/HTTP/Gecko_user_agent_string_reference

You can find fake UA here: http://www.useragentstring.com/pages/useragentstring.php. Please, don't choose very original string but search some average values as described here.

**Attention:** To prevent UA-leaks you must change UA-string with globally disabled JavaScript!


- LOCALE, LANGUAGES

Switch browser's local from national to English:

    general.useragent.locale=en-US

http://kb.mozillazine.org/General.useragent.locale

Ignore the OS’s locale and use the value from general.useragent.locale:

    intl.locale.matchOS=false

http://kb.mozillazine.org/Intl.locale.matchOS

Reset list of preferred languages to en-US/en:

    intl.accept_languages=en-US, en

Switch off spellchecker: 

    layout.spellcheckDefault=0

http://kb.mozillazine.org/Layout.spellcheckDefault

Specifying the heuristic detection mode. Determines which locale URI sets how character set are detected in the browser. Stay this field empty. The setting must be left blank for all locales other than Russian (=ruprobe), Ukrainian and Japanese. Do not under any circumstances specify the "universal" detector.

    intl.charset.detector=

Do not change in Firefox Mobile:

    intl.charset.detector=chrome://global.locale/intl.properties  (Android)

Different languages: 

http://www-archive.mozilla.org/projects/intl/chardet.html

Additional information:

https://developer.mozilla.org/en-US/docs/Web/Guide/Localizations_and_character_encodings

**Attention:** We strongly recommend to install English version of Firefox!

**Attention:** To prevent locale-leaks you must deny JavaScript globally!


- REFERERS

Referer is an HTTP-header field that identifies URI that linked to the resource being requested. By checking the referrer, the server can see where the request originated. When a user clicks a hyperlink, the browser sends a request to the server holding the destination web page. The request includes the referrer, which indicates the last site/page the user was on. Referer logging is used to allow servers to identify where users are visiting them from, for promotional or statistical purposes.

Never send the Referer header:

    network.http.sendRefererHeader=0 (recommended)

Send the Referer header when clicking on a link or loading an image, and set document.referrer for the following page:

    network.http.sendRefererHeader=1 (not recommended)

http://kb.mozillazine.org/Network.http.sendRefererHeader

Don't send the Referer header when navigating from a HTTPS site to another HTTPS site:

    network.http.sendSecureXSiteReferrer=false (maybe obsolete)

http://kb.mozillazine.org/Network.http.sendSecureXSiteReferrer


- REDIRECTIONS

Servers can send redirects - an instruction that the browser should try to get the content from another URL. Because one URL could redirect to another and the other could redirect to the first, causing an infinite loop, a limit is placed on how many redirects can occur on one request.

Set the limit of redirections to another page without user's decision:

    network.http.redirection-limit=1

Notify about the end of limit:

    network.http.prompt-temp-redirect=true

http://kb.mozillazine.org/Network.http.redirection-limit


- AUTOREFRESH

Prevent autorefresh of webpage or redirects to another page:

    accessibility.blockautorefresh=true

http://kb.mozillazine.org/Accessibility.blockautorefresh


- POPUPS

Popups blocking and enabling info message when pop-ups are blocked:

    dom.disable_open_during_load=true
    browser.popups.showPopupBlocker=true

http://kb.mozillazine.org/Pop-ups_not_blocked

https://support.mozilla.org/en-US/questions/675692

To get around the default popup blocker, some sites use Flash or Java applets to open unrequested windows. This preference controls popups initiated by plugins. Block all plugin initiated popups:

    privacy.popups.disable_from_plugins=2

http://kb.mozillazine.org/Privacy.popups.disable_from_plugins


- IMAGES, FAVICONS

Block all images from loading. The permissions extension allows for a more complete method of allowing, blocking, and restricting content displayed in the browser-including images:

    permissions.default.image=2 (recommended)

Load images from original site only. Prevent third-party images from loading: 

    permissions.default.image=3 (not recommended)

http://kb.mozillazine.org/Permissions.default.image

Prevent image animation (*.gif, etc.):

    image.animation_mode=none

http://kb.mozillazine.org/Firefox_:_Tips_:_Animated_Images

Suppress the display of site icons. Display the default Mozilla “document” icon instead: 

    browser.chrome.site_icons=false
    browser.chrome.favicons=false

http://kb.mozillazine.org/Browser.chrome.site_icons

http://kb.mozillazine.org/Browser.chrome.favicons


- PASSWORDS, FORMS

Don't save any logins and passwords:

    signon.rememberSignons=false
    signon.storeWhenAutocompleteOff=false

https://support.mozilla.org/en-US/questions/889884

Do not automatically fill sign-in forms with known usernames and passwords; instead, act as though there are multiple usernames/password pairs remembered for the form (fill password after username has been manually typed): 

    signon.autofillForms=false

http://kb.mozillazine.org/Signon.autofillForms

Block password's synchronisation through Firefox Sync:

    services.sync.prefs.sync.signon.rememberSignons=false

Block formfill. Firefox can't remember what you've entered in forms on web pages, also known as text fields. After you've entered something into a form on a web page (such as a search box), the next time you visit that page, your previous entry will be not available to re-use:

    browser.formfill.enable=false
    browser.formfill.expire_days=0
    browser.formfill.saveHttpsForms=false

https://support.mozilla.org/en-US/questions/813403

Block form's synchronization through Firefox Sync:

    services.sync.prefs.sync.browser.formfill.enable=false


- NETWORK: PIPELINING, DNS, PREFETCH, PING, SSl

Enable or disable pipelining. In HTTP multiple requests can be sent before any responses are received. This is known as pipelining. Pipelining reduces network load and can reduce page loading times over high-latency connections, but not all servers support it.

Attempt to use pipelining in HTTP 1.1 connections. Disable ssl-pipelining:

    network.http.pipelining=true
    network.http.pipelining.ssl=false
    network.http.version=1.1 (don't create: it's default)

http://kb.mozillazine.org/Network.http.pipelining

http://kb.mozillazine.org/Network.http.pipelining.ssl

http://kb.mozillazine.org/Network.http.version

Attempt to use pipelining through proxy-server:

    network.http.proxy.pipelining=true
    network.http.proxy.version=1.1 (don't create: it's default)

http://kb.mozillazine.org/Network.http.proxy.keep-alive

http://kb.mozillazine.org/Network.http.proxy.version

Check this settings to keep-alive pipelining:

    network.http.keep-alive=true

http://kb.mozillazine.org/Network.http.keep-alive

Sen maximum number of pipelining requests:

    network.http.pipelining.maxrequests=32 (don't create: it's default; recommended)

http://kb.mozillazine.org/Network.http.pipelining.maxrequests

Block DNS prefetching. DNS prefetching was implemented to improve page load time. This feature allows Firefox to perform domain name resolution proactively and in parallel for hyperlinks, images, CSS, JavaScript, and other web page content:

    network.dns.disablePrefetch=true

http://kb.mozillazine.org/Network.dns.disablePrefetch

Block DNS prefetching on https-page:

    network.dns.disablePrefetchFromHTTPS=true (maybe obsolete or Android only)

Block link prefetching. Link prefetching is when a web page hints to the browser that certain pages are likely to be visited, so the browser downloads them immediately so they can be displayed immediately when the user requests it: 

    network.prefetch-next=false

http://kb.mozillazine.org/Network.prefetch-next

Allow remote DNS. This preference controls whether DNS lookups for SOCKS v5 clients happen on the client or on the proxy server. To bypass your default DNS-server, switch to: 

    network.proxy.socks_remote_dns=true

http://kb.mozillazine.org/Network.proxy.socks_remote_dns

Block DNS-resolving over IPv6:

    network.dns.disableIPv6=true

Ignore the ping attribute. HTML5 defines a new attribute for <a> elements: ping. This attribute contains one or more URIs to "ping" (send a POST request to) when the user clicks the link. The attribute would be useful for letting websites track visitors’ clicks:

    browser.send_pings=false
    browser.send_pings.require_same_host=false

http://kb.mozillazine.org/Browser.send_pings

Block support for Network API, which can determine the type of connection, network parameters such as the current bandwidth of the user's device:

    dom.netinfo.enabled=false

https://developer.mozilla.org/en-US/docs/Web/API/Navigator/connection

Block beacon leaks. A web beacon is an object embedded in a web page or email, which unobtrusively (usually invisibly) allows checking that a user has accessed the content. Common uses are email tracking and page tagging for web analytic:

    beacon.enabled=false

https://en.wikipedia.org/wiki/Web_beacon

Block non-safe algorithms (SSL3):

    security.ssl3.ecdhe_ecdsa_rc4_128_sha=false
    security.ssl3.ecdhe_rsa_rc4_128_sha=false
    security.ssl3.rsa_rc4_128_md5=false
    security.ssl3.rsa_rc4_128_sha=false
    security.ssl3.rsa_des_ede3_sha=false


- PORTS

**Attention: DO NOT change settings in this part if you don't understand what you are doing!**

To retrieve data, Mozilla can be configured to route its requests through another local server, e.g. Polipo and another software:

    network.proxy.type=1 (ON, manual proxy configuration - for example: Polipo)

or:

    network.proxy.type=0 (OFF, direct internet connection)

http://kb.mozillazine.org/Network.proxy.type

If proxy ON (for example: Polipo), you must set HTTP, SSL, FTP protocols to:

HTTP:

    network.proxy.http=localhost
    network.proxy.http_port=8118
    
SSL:

    network.proxy.ssl=localhost
    network.proxy.ssl_port=8118
    
FTP:

    network.proxy.ftp=localhost
    network.proxy.ftp_port=8118

https://developer.mozilla.org/en-US/docs/Mozilla/Preferences/Mozilla_networking_preferences

Remote DNS. This preference controls whether DNS lookups for SOCKS v5 clients happen on the client or on the server:

    network.proxy.socks_remote_dns=true

http://kb.mozillazine.org/Network.proxy.socks_remote_dns

SOCKS:

    network.proxy.socks_version=5 (don't create: it's default)
    network.proxy.socks=localhost
    network.proxy.socks_port=9050

http://kb.mozillazine.org/Network.proxy.socks_version

http://kb.mozillazine.org/Network.proxy.socks_port

No proxy for localhost. Many networks had limited access to the public network via proxy servers. This preference was originally designed as a "black-list" of sites or domains that was within the intranet, and should not be accessed via the proxy server: 

    network.proxy.no_proxies_on=localhost, 127.0.0.1

http://kb.mozillazine.org/Network.proxy.no_proxies_on

Banned ports. Some port numbers are reserved for functions such as e-mail or FTP. To prevent potential security risks if a protocol was allowed access a port reserved for a separate protocol, Firefox contain a list of banned ports, for example:

    network.security.ports.banned=9050,9051,9150,9151,8118,4444

http://kb.mozillazine.org/Network.security.ports.banned


- MULTIMEDIA

Block Mozilla Video Statistics API extensions:

    media.video_stats.enabled=false

https://developer.mozilla.org/en-US/docs/Web/API/HTMLVideoElement#Gecko-specific_properties

Block WebGL (if you have some problems with video, other hardware, etc.):

    webgl.disable-extensions=true
    webgl.disabled=true
    webgl.force-enabled=false
    webgl.min_capability_mode=true

Deny OffscreenCanvas. The OffscreenCanvas interface provides a canvas that can be rendered off screen. It is available in both, the window and in a worker context. This API is currently implemented for WebGL1 and WebGL2 contexts only. Switch to:

    gfx.offscreencanvas.enabled=false (FF 44 and higher)

https://developer.mozilla.org/en-US/docs/Web/API/OffscreenCanvas

Don’t load media plugins until they’re clicked:

    plugins.click_to_play=true

Block media autoplay:

    media.autoplay.enabled=false
    media.audio_data.enabled=false (maybe obsolete)

Block codecs:

    media.ogg.enabled=false
    media.opus.enabled=false
    media.raw.enabled=false
    media.wave.enabled=false
    media.webm.enabled=false
    media.webvtt.enabled=false
    media.gmp-gmpopenh264.provider.enabled=false
    media.gmp-provider.enabled=false
    media.webaudio.enabled=false  (maybe obsolete)

https://support.mozilla.org/en-US/questions/992868

Block Web Speech API. The Web Speech API has two parts: SpeechSynthesis (Text-to-Speech), and SpeechRecognition (Asynchronous Speech Recognition):

    media.webspeech.recognition.enable=false
    media.webspeech.synth.enabled=false

https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API


- PLUGINS (FLASH, JAVA)

Deny plugins. A plugin is a piece of software that displays internet content that Firefox is not designed to display. This usually includes video, audio, online games and presentations that are made in patented (proprietary, non-free) formats: Adobe Flash, Apple QuickTime, Microsoft Silverlight; special software for download. 

Plugin's policy. To deny all, set:

    plugin.default.state=0
    plugins.update.url=
    pfs.datasource.url=

Firefox mobile:

    media.plugins.enabled=false  (Android)
    plugin.disable=true  (Android)

https://support.mozilla.org/en-US/questions/1002509

To deny one, set:

    plugin.state.flash=0 
    plugin.state.java=0
    plugin.state.quicktime=0

Permissible settings:

    plugin.state.название_плагина=0 (blocked);
    plugin.state.название_плагина=1 (ask);
    plugin.state.название_плагина=2 (always on).

Deny Plugin-container. Each plugin are loaded separately from Firefox in a plugin-container.exe process, allowing the main Firefox process (firefox.exe) to stay open if a plugin crashes. Plugin-container needs a lot of RAM:

    dom.ipc.plugins.enabled=false (maybe not work)

https://support.mozilla.org/en-US/kb/what-is-plugin-container

Block reports about plugin-container's crashes (needs to flash-player):

    dom.ipc.plugins.flash.subprocess.crashreporter.enabled=false
    dom.ipc.plugins.reportCrashURL=false

https://support.mozilla.org/en-US/kb/send-plugin-crash-reports-help-improve-firefox

Stop message "Would you like to install the plugin needed to display the media on this page":

    plugins.hideMissingPluginsNotification=true
    plugins.notifyMissingFlash=false

https://support.mozilla.org/en-US/questions/969127

- SESSIONS, HISTORY

Block Session Restore service completely. Firefox has a built-in Session Restore feature, allowing the user to continue browsing from where they left off if browser restarts. This preference controls when to store extra information about a session: contents of forms, scrollbar positions, cookies, and POST data:

    browser.sessionstore.enabled=false

http://kb.mozillazine.org/Browser.sessionstore.enabled

Block session store. Never store extra session data:

    browser.sessionstore.privacy_level=2

http://kb.mozillazine.org/Browser.sessionstore.privacy_level

Block session store on standard reload. Controls what gets saved by Session Restore when quitting (not crashing or restarting to install updates/addons):

    browser.sessionstore.privacy_level_deferred=2

http://kb.mozillazine.org/Browser.sessionstore.privacy_level

Controls how many closed tabs are kept track of via the Session Restore service:
 
    browser.sessionstore.max_tabs_undo=0

http://kb.mozillazine.org/Browser.sessionstore.max_tabs_undo

Controls how many closed windows are kept track of via the Session Restore service:

    browser.sessionstore.max_windows_undo=0

http://kb.mozillazine.org/Browser.sessionstore.max_windows_undo

Don't resume session at the next application start, but not again:

    browser.sessionstore.resume_session_once=false

http://kb.mozillazine.org/Browser.sessionstore.resume_session_once

Don't resume sessions post-crash:

    browser.sessionstore.resume_from_crash=false

http://kb.mozillazine.org/Browser.sessionstore.resume_from_crash

Define the maximum number of pages in the browser's session history, i.e. the maximum number of URLs you can traverse purely through the Back/Forward buttons: 

    browser.sessionhistory.max_entries=5

https://wiki.mozilla.org/Firefox/session_restore

Pages that were recently visited are stored in memory in such a way that they don't have to be re-parsed (this is different from the memory cache). This improves performance when pressing Back and Forward:
 
"-1" - Automatically determine the maximum amount of pages to store in memory based on the total amount of RAM:

    browser.sessionhistory.max_total_viewers=-1 (default; recommended)

http://kb.mozillazine.org/Browser.sessionhistory.max_total_viewers

Number of crashes that can occur before the about:sessionrestore page is displayed:

    browser.sessionstore.max_resumed_crashes=0

http://kb.mozillazine.org/Browser.sessionstore.max_resumed_crashes

https://wiki.mozilla.org/Firefox/session_restore

Block history and history of downloads in Places. Places is a system for storing bookmarks, history, and other user information about the Web: 

    places.history.enabled=false

https://wiki.mozilla.org/Places

Block Location Bar's autocomplete (numbers of dropdown lines with offered results). The Location Bar (also called the URL or address bar), the Search Bar, and some form fields on web pages have autocomplete dropdowns that appear with a list of previously-entered data:

    browser.urlbar.maxRichResults=0

http://kb.mozillazine.org/Browser.urlbar.maxRichResults

Block data's autocomplete from places and bookmarks:

    browser.urlbar.autocomplete.enabled=false

http://kb.mozillazine.org/Changing_autocomplete_behavior_-_Firefox

Reduce number of bookmark's backups:

    browser.bookmarks.max_backups=1

http://kb.mozillazine.org/Browser.bookmarks.max_backups


- CACHE

**Attention:** If you have Firefox for Android or for iOS (RAM less than 2 Gb), don't change any settings!

Don't cache HTTP or HTTPS files:

    network.http.use-cache=false

http://kb.mozillazine.org/Network.http.use-cache

Don't store cache on the hard drive:

    browser.cache.disk.enable=false

http://kb.mozillazine.org/Browser.cache.disk.enable

Pages transmitted with SSL encryption often contain sensitive information and caching of these pages to disk may present a privacy risk. Switch to: 

    browser.cache.disk_cache_ssl=false

http://kb.mozillazine.org/Browser.cache.disk_cache_ssl

Don't store offline cache on the hard drive:

    browser.cache.offline.enable=false

http://kb.mozillazine.org/Browser.cache.offline.enable

Block smart sizing of the disk cache:

    browser.cache.disk.smart_size.enabled=false

https://developer.mozilla.org/en-US/docs/Mozilla/Preferences/Mozilla_networking_preferences#Cache

Set cache to zero. Do not cache files on the hard drive: 

    browser.cache.disk.capacity=0
    browser.cache.offline.capacity=0

http://kb.mozillazine.org/Browser.cache.disk.capacity

**Attention:** Switch "browser.cache.disk.smart_size.enabled" to false.

Allow decoded images, chrome, and secure pages to be cached in memory.

    browser.cache.memory.enable=true

http://kb.mozillazine.org/Browser.cache.memory.enable

Automatically decide the maximum memory to use to cache decoded images, messages, and chrome based on the total amount of RAM.

    browser.cache.memory.capacity=-1 (default; recommended)

Possible values:

"0" - Do not cache decoded images and chrome in memory (not recommended; see below);

Any positive integer - maximum amount of memory in KB to use to cache decoded images and chrome (1 MB = 1024 KB).

Atention: Switch "browser.cache.memory.enable" to true.

http://kb.mozillazine.org/Browser.cache.memory.capacity

**Attention:** If you want to disable cache in RAM and(!) on HDD, it's big mistake!


- GEO-IP

Deny Geo. Firefox has a feature that allows sites to request your location (e.g., to allow those sites to show your location on a map). If a site requests your location, Firefox seeks your permission before determining and sharing your location. In order to determine your location, Firefox may use several pieces of data to determine your location, including your operating systems geolocation features, Wi-Fi networks, cell phone towers, or IP address. Estimating your location involves sending some of this information to Google's geolocation service. Switch to:

    geo.enabled=false
    geo.wifi.uri=
    browser.geolocation.warning.infoURL=

https://www.mozilla.org/en-US/firefox/geolocation/


- SEARCH: GEO-IP

Firefox sends Mozilla a request once to look up your location at a country level using your IP address. Then Mozilla send that country level information back to Firefox, where it's stored locally. Firefox will then choose which search engine to use as its default based on the locally stored country information.

Deny Search Suggestions. Search suggestions is a feature to find out common phrases that other people have searched for. These search suggestions are offered by your Default Search Engines (such as Google, Yahoo, etc.) and not by Firefox. If you enable this feature, and your Default Search Engine supports suggestions, Firefox may send the terms you type in the Awesome Bar or Search Bar to your Default Search Engine to retrieve suggestions, and is governed by the applicable Privacy Policy from your Default Search Engine. To disable search suggestions, switch to: 

    browser.search.suggest.enabled=false

http://kb.mozillazine.org/Browser.search.suggest.enabled

Deny GEO-search. In order to set the right default search engine for your location, Firefox will perform a geolocation lookup once by contacting Mozilla's servers and store the country-level result locally. In order to determine your location, Firefox may use several pieces of data to determine your location, including your operating systems, geolocation features, Wi-Fi networks, cell phone towers, or IP address. To disable GEO-search, switch to: 

    browser.search.geoSpecificDefaults=false
    browser.search.geoip.url=false (maybe obsolete)
    browser.search.countryCode=US (maybe obsolete)
    browser.search.region=US (maybe obsolete)

https://support.mozilla.org/en-US/kb/how-stop-firefox-making-automatic-connections


- UPDATES: BROWSER, PERSONAS, SEARCH PLUGINS

Block browser's automatic updates. Once per day, Firefox sends the following info to Mozilla when it checks for browser updates: your Firefox version information, language preference, operating system, version and automatically download and install available updates.  Switch to:

    app.update.auto=false
    app.feedback.baseURL=
    app.support.baseURL=
    app.update.url=
    app.update.url.details=
    app.update.url.manual=

Block browser's search plugins automatic updates:

    browser.search.update=false

Block Personas automatic updates. Firefox have native support for lightweight themes. Such themes allow to make changes to the default theme and do not replace that theme completely like regular themes do. Personas are an example of such a lightweight theme. Switch to:

    lightweightThemes.update.enabled=false
    lightweightThemes.getMoreURL=
    lightweightThemes.recommendedThemes=

http://kb.mozillazine.org/Themes

Block milestone info. When a user starts up their browser, this preference is examined. If its value differs from the browser’s current milestone, then the user is redirected to special homepage and this preference’s value is updated to the current milestone. Switch to: 

    browser.startup.homepage_override.mstone=ignore

http://kb.mozillazine.org/Browser.startup.homepage_override.mstone

Don't heck the system default browser on startup. Check to see if the browser is set as default; if not, ask if the user wants it set that way. Do not perform this check:

    browser.shell.checkDefaultBrowser=false

http://kb.mozillazine.org/About:config_entries


- UPDATES: ADDONS

Block browser's addons automatic updates. Firefox sends the following info to Mozilla when it checks for browser's addons updates: your Firefox version information, language preference, operating system, version and automatically download and install available updates. Switch to:

    extensions.update.autoUpdateDefault=false
    extensions.update.enabled=false
    extensions.update.url=

http://kb.mozillazine.org/About:config_entries#Extensions.

Firefox offers a Get Add-ons page of the Add-ons Manager that features popular add-ons and displays personalized recommendations based on the add-ons you already have installed. To display the personalized recommendations, Firefox sends information to Mozilla, including the list of add-ons you have installed, Firefox version information, and your IP address. Switch to:

    extensions.getAddons.cache.enabled=false

https://blog.mozilla.org/addons/how-to-opt-out-of-add-on-metadata-updates/

Firefox 3’s Add-ons dialog integrates with addons.mozilla.org to allow users to search and install extensions and themes. The functionality is available in the “Get Addons” pane. Block it: 

    extensions.getAddons.recommended.url=
    extensions.getAddons.getWithPerformance.url=
    extensions.webservice.discoverURL=

http://kb.mozillazine.org/Extensions.getAddons.recommended.url

Deny Addons Blocklist. Firefox contacts Mozilla to check for malicious addons. Specific extensions can be blocklisted from a central server. The blocklist is not only used for malicious extensions but also to disable vulnerable plugins & crash-prone graphic drivers. Switch to:

    extensions.blocklist.enabled=false
    extensions.blocklist.itemURL=
    extensions.blocklist.url=
    extensions.blocklist.detailsURL=

http://kb.mozillazine.org/Extensions.blocklist.enabled

**Attention:** You don't need any addons in the current Firefox's configuration! But if you really want to install some addons, you can find trusted versions here: https://www.gnu.org/software/gnuzilla/addons.html

**Attention:** Addon's can probably override current browser settings!


- CLEAN

Perform the Clear Private Data operation when closing the browser: 

    privacy.sanitize.sanitizeOnShutdown=true

(additional settings):

    privacy.clearOnShutdown.cache=true
    privacy.clearOnShutdown.cookies=true
    privacy.clearOnShutdown.downloads=true
    privacy.clearOnShutdown.formdata=true
    privacy.clearOnShutdown.history=true
    privacy.clearOnShutdown.offlineApps=true
    privacy.clearOnShutdown.passwords=true
    privacy.clearOnShutdown.sessions=true
    privacy.clearOnShutdown.siteSettings=true
    privacy.clearOnShutdown.sessions=true

http://kb.mozillazine.org/About:config_entries


- DOWNLOADS/OPEN

Do not scan downloads for viruses. If a Windows user has an antivirus program installed, it is launched to scan files when they finish downloading. Internet security software, including firewalls, antivirus programs, anti-spyware programs, and others can block certain file downloads. Downloading an executable file (e.g., an *.exe or *.msi file) may fail, with the Downloads window showing Canceled under the file name. This happens because Firefox honors your Windows security settings for downloading applications and other potentially unsafe files from the Internet. Switch to:

    browser.download.manager.scanWhenDone=false

http://kb.mozillazine.org/Browser.download.manager.scanWhenDone

https://support.mozilla.org/en-US/kb/cant-download-or-save-files

Do not add downloaded files to Recent Documents:

    browser.download.manager.addToRecentDocs=false

https://developer.mozilla.org/en-US/docs/Download_Manager_preferences

http://kb.mozillazine.org/Browser.download.manager.addToRecentDocs

Restrict jar: to files served with the proper Content-Types (*.jar, *.zip, etc.). Mozilla supports the jar: protocol, which allows the browser to directly load files inside JAR archives (and other files based on ZIP). Unfortunately, this feature can open up cross-site scripting issues on otherwise secure sites, by allowing script content to be loaded inside pages with the same permissions as the page itself. Switch to:

    network.jar.open-unsafe-types=false

http://kb.mozillazine.org/Network.jar.open-unsafe-types


- SERVICES, TELEMETRY

- DNT, TRACKING PROTECTION

Most major websites track their visitors' behavior and then sell or provide that information to other companies. This information can be used to show ads, products or services specifically targeted to you. Firefox has a Do Not Track feature that lets you tell every website you visit, their advertisers, and content providers that you don't want your browsing behavior tracked. Honoring this setting is voluntary - individual websites are not required to respect it. As a rule, owners of tracking sites have very aggressive policy and activity, that is why DNT is very useless function. To switch off:

    privacy.donottrackheader.enabled=false
    privacy.donottrackheader.value=1

http://kb.mozillazine.org/Privacy.donottrackheader.enabled

http://kb.mozillazine.org/Privacy.donottrackheader.value

https://support.mozilla.org/en-US/kb/how-do-i-turn-do-not-track-feature

Firefox include built-in tracking protection. In Private Browsing windows (tabs, in Firefox for Android), Firefox will block content loaded from domains that track users across sites. Firefox will ship with a list of sites which have been identified as engaging in cross-site tracking of users. When tracking protection is enabled, Firefox will block content from sites in the list. But you have a potential risk to disclose own preferences (web-activity). Block this function:

    privacy.trackingprotection.enabled=false
    browser.trackingprotection.gethashURL=
    browser.trackingprotection.updateURL=

https://developer.mozilla.org/en-US/Firefox/Privacy/Tracking_Protection


- POCKET

The propietary application Pocket (previously known as "Read It Later") allows the user to save an article or web page to the cloud for later reading. The article is then sent to the user's Pocket list (synced to all of their devices) for offline reading. You have a potential risk to disclose own preferences (web-activity). Deny it:

    browser.pocket.enabled=false

**Attention:** Unfortunately, this setting don't disable service but block Pocket's button only.


- GOOGLE

Block Google's SafeBrowsing. About twice per hour, Firefox downloads Google's SafeBrowsing lists to help block access to sites and downloads that are malicious or forged. For downloaded executables that do not appear in these lists, Firefox may send metadata, including URLs associated with the downloaded file, to the SafeBrowsing service. You have a potential risk to disclose own preferences (web-activity). Do not use blacklists from Goggle and do not check downloads: 

    browser.safebrowsing.enabled=false
    browser.safebrowsing.malware.enabled=false
    browser.safebrowsing.downloads.enabled=false
    browser.safebrowsing.downloads.remote.enabled=false
    services.sync.prefs.sync.browser.safebrowsing.enabled=false
    services.sync.prefs.sync.browser.safebrowsing.malware.enabled=false
    browser.safebrowsing.appRepURL=
    browser.safebrowsing.gethashURL=
    browser.safebrowsing.malware.reportURL=
    browser.safebrowsing.reportErrorURL=
    browser.safebrowsing.reportGenericURL=
    browser.safebrowsing.reportMalwareErrorURL=
    browser.safebrowsing.reportMalwareURL=
    browser.safebrowsing.reportPhishURL=
    browser.safebrowsing.reportURL=
    browser.safebrowsing.updateURL=

http://kb.mozillazine.org/Browser.safebrowsing.enabled

http://kb.mozillazine.org/Browser.safebrowsing.malware.enabled


- SYNC

Deny Firefox Sync. Firefox Sync is a set of software components and specifications that synchronize data (bookmarks, passwords, tabs and more) between multiple Mozilla product instances. Transmission of user's data (especially logins, passwords, cookies) outside of device (through Mozilla's servers) is very dangerous! Switch to:

    services.sync.serverURL=
    services.sync.tokenServerURI=
    services.push.serverURL=
    services.sync.fxa.privacyURL=
    services.sync.fxa.termsURL=
    services.sync.jpake.serverURL=
    services.sync.privacyURL=
    services.sync.statusURL=
    services.sync.syncKeyHelpURL=
    services.sync.termsURL=
    identity.fxaccounts.auth.uri=
    identity.fxaccounts.remote.force_auth.uri=
    identity.fxaccounts.remote.signin.uri=
    identity.fxaccounts.remote.signup.uri=
    identity.fxaccounts.settings.uri=
    services.sync.engine.addons=false
    services.sync.engine.bookmarks=false
    services.sync.engine.history=false
    services.sync.engine.passwords=false
    services.sync.engine.prefs=false
    services.sync.engine.tabs=false

https://wiki.mozilla.org/Services/Sync/Addon_Sync


- MARKETPLACE

Block Firefox Marketplace (marketplace for web apps):

    browser.apps.URL=
    dom.mozApps.signed_apps_installable_from=

https://support.mozilla.org/en-US/questions/1064312


- PDF

Block PDF view in browser. This is an HTML5 technology experiment that explores building a faithful and efficient Portable Document Format (PDF) renderer without native code assistance. Switch to: 

    pdfjs.disabled=true

https://support.mozilla.org/en-US/questions/943119


- FONTS

Deny to downloading web-fonts. The major concern with the introduction of this feature is that it exposes our text rendering code and the platform-specific libraries we use to attack via intentionally corrupt fonts. Possible risk areas: handling font names, reading the character map, handling metrics, catching errors when drawing with bogus glyph data. Switch to:

    gfx.downloadable_fonts.enabled=false
    gfx.downloadable_fonts.woff2.enabled=false
    gfx.font_rendering.opentype_svg.enabled=false

https://wiki.mozilla.org/Firefox3.1/Downloadable_Fonts_Security_Review


- TILES

Deny Tiles advertisement. Tiles are a feature of Firefox displayed on new tab pages. In order to provide the tiles feature, Firefox sends to Mozilla data relating to the tiles such as number of clicks, impressions, your IP address, locale information, and tile specific data (e.g., position and size of grid). Telemetry experiments for Tiles may collect information about commonly visited domains. The list of default tiles given to new users is built from popular tiles and other tiles Mozilla chooses. Firefox periodically downloads a list of tiles to use as default tiles, based on basic information such as the user locale and geographic location (determined by IP address). Switch to: 

    browser.newtabpage.directory.ping=
    browser.newtabpage.directory.source=

https://support.mozilla.org/en-US/questions/1074600

Block thumbnails/screenshots. The preference disabled controls whether the application creates screenshots of visited pages which will be shown if the web page is shown in the grid of the "New Tab Page" (about:newtab) which offers the most often visited pages for fast navigation:

You must(!) create two boolean strings (if they are not present):

    browser.pagethumbnails.capturing_disabled=true
    pageThumbs.enabled=false

https://developer.mozilla.org/en-US/docs/Mozilla/Preferences/Preference_reference/browser.pagethumbnails.capturing_disabled

https://support.mozilla.org/en-US/questions/973320


- SNIPPETS

Deny snippets. Firefox's default home page (about:home) loads small bits of information right below the search bar that we think will be useful to you. We call these "snippets". About once per day, Firefox connects to Mozilla and provides you with new snippets, if available. Mozilla may collect how often snippets are clicked, snippet name, browser locale, and which version of Firefox you're using. We only retain this information after 60 days in aggregate form. To help display relevant snippets, Firefox sends Mozilla a monthly request to look up your location at a country level using your IP address. Then Mozilla send that country level information back to Firefox, where it's stored locally. Firefox will then choose snippets to show you based on the locally stored country information. Some Mozilla sponsored snippets are interactive and allow you to optionally share your phone number or email address. It's very dangerous and must be disabled:

    browser.aboutHomeSnippets.updateUrl=
    browser.snippets.countryCode=US (Android)
    browser.snippets.enabled=false  (Android)
    browser.snippets.syncPromo.enabled=false  (Android)
    browser.snippets.geoUrl=  (Android)
    browser.snippets.statsUrl=  (Android)
    browser.snippets.updateUrl=  (Android)

https://wiki.mozilla.org/Firefox/Projects/Firefox_Start/Snippet_Service


- WebRTC

Deny WebRTC. WebRTC (Web Real-Time Communication) is an API definition drafted by the World Wide Web Consortium (W3C) that supports browser-to-browser applications for voice calling, video chat, and P2P file sharing without the need of either internal or external plugins. Switch to:

    media.peerconnection.enabled=false
    media.peerconnection.identity.enabled=false
    media.peerconnection.video.enabled=false
    media.websocket.enabled=false (maybe obsolete)

http://kb.mozillazine.org/About:config


- HELLO

Block Firefox Hello. Firefox Hello lets you have free video and voice calls and text messaging directly in the browser. Switch to:

    loop.enabled=false
    loop.throttled2=false
    loop.feedback.baseUrl=
    loop.gettingStarted.url=
    loop.learnMoreUrl=
    loop.legal.ToS_url=
    loop.legal.privacy_url=
    loop.oauth.google.redirect_uri=
    loop.oauth.google.scope=
    loop.server=
    loop.soft_start_hostname=
    loop.support_url=
    loop.rooms.enabled=false
    loop.CSP=

https://support.mozilla.org/en-US/kb/firefox-hello-video-and-voice-conversations-online

https://support.mozilla.org/en-US/questions/1043588


- SPDY

Deny SPDY. SPDY is an open networking protocol developed primarily at Google for transporting web content. SPDY manipulates HTTP traffic, with particular goals of reducing web page load latency and improving web security. SPDY achieves reduced latency through compression, multiplexing, and prioritization, although this depends on a combination of network and website deployment conditions. Switch to:

    network.http.spdy.allow-push=false
    network.http.spdy.enabled=false
    network.http.spdy.enabled.http2=false
    network.http.spdy.enabled.http2draft=false
    network.http.spdy.enabled.v3=false
    network.http.spdy.enabled.v3-1=false
    media.http.spdy.enabled=false
    network.http.spdy.enabled.deps=false (maybe obsolete or absent)

https://en.wikipedia.org/wiki/SPDY


- TELEMETRY

Deny Telemetry. Usage statistics or "Telemetry" is a feature in Firefox that sends Mozilla usage, performance, and responsiveness statistics about user interface features, memory, and hardware configuration. Your IP address is also collected as a part of a standard web log. Usage statistics are transmitted using SSL and help us improve future versions of Firefox. Once sent to Mozilla, usage statistics are aggregated and made available to a broad range of developers, including both Mozilla employees and public contributors. When Telemetry is enabled, certain short-term experiments may collect information about visited sites. It's very dangerous and must be disabled. Switch to:

    toolkit.telemetry.server=
    toolkit.telemetry.enabled=false
    toolkit.identity.enabled=false
    toolkit.crashreporter.infoURL=
    toolkit.telemetry.infoURL=

https://wiki.mozilla.org/Telemetry/faq


- TELEMETRY: EXPERIMENTS

Deny Experiments. Telemetry Experiments is a feature that allows Firefox to automatically download and run specially-designed restartless addons based on certain conditions. Switch to:

    app.update.lastUpdateTime.experiments-update-timer=0
    experiments.enabled=false
    experiments.manifest.fetchIntervalSeconds=0
    experiments.manifest.uri=
    experiments.supported=false
    network.allow-experiments=false
    experiments.logging.dump=false (maybe absent)

https://wiki.mozilla.org/Telemetry/Experiments


- HEALTH REPORT (FHR)

Deny Firefox Health Report. Firefox Health Report (FHR) is designed to provide you with insights about your browser's stability and performance and with support tips should you experience issues, such as high crash rates or slow startup times. Mozilla collects and aggregates your data with that of other Firefox users and sends it back to your browser so you can see how your Firefox performance changes over time. This data includes, for example: device hardware, operating system, Firefox version, add-ons (count and type), timing of browser events, rendering, session restores, length of session, how old a profile is, count of crashes, and count of pages. This is a serious source of leaks. Switch to:

    datareporting.healthreport.service.firstRun=false
    datareporting.healthreport.service.enabled=false
    datareporting.healthreport.uploadEnabled=false
    datareporting.policy.dataSubmissionEnabled=false
    datareporting.healthreport.logging.dumpEnabled=false
    datareporting.healthreport.infoURL=
    datareporting.healthreport.documentServerURI=
    datareporting.healthreport.about.reportUrl=

https://support.mozilla.org/en-US/questions/1078303


- CRASH REPORTING

Deny crash reporting. This is the option to send Mozilla a crash report after Firefox crashes. This report contains technical information for us to improve Firefox including why Firefox crashed, the active URL at time of crash, and the state of computer memory during the crash. The crash report we receive may include personal information. Switch to:

    breakpad.reportURL=


- HEARTBEAT

Deny Heartbeat. Heartbeat is User Voice in Firefox. Heartbeat provides real-time understanding of our existing Desktop user population, allowing us to pivot more quickly based on the needs and desires of our users. Heartbeat ties user perception to technical information so we can take your feedback and feed that into future Firefox releases. Switch to:

    browser.selfsupport.url= (maybe Android only)

https://wiki.mozilla.org/Advocacy/heartbeat


- PREDICTOR (ex-SEER)

Deny network predictor (seer). The network predictor (formerly called "seer") makes preemptive connections to resources in a page based on cached information. It can also do the same when the user hovers over a link - to improve page load time by performing overhead for connections before the connections are actually needed. Firefox predicts where you will click next or what you will do next, and begins to process this in advance to speed up the process if you make the predicted move. Switch to:

    network.seer.enabled=false (maybe obsolete or absent)
    network.seer.max-db-size=0 (maybe obsolete or absent)
    network.predictor.enabled=false
    network.predictor.enable-hover-on-ssl=false
    network.predictor.max-db-size=0

To improve the loading speed, Firefox will open predictive connections to sites when the user hovers their mouse over thumbnails on the New Tab Page or the user starts to search in the Search Bar, or in the search field on the Home or the New Tab Page. To disable this feature, set: 

    network.http.speculative-parallel-limit=0

https://support.mozilla.org/en-US/kb/how-stop-firefox-making-automatic-connections#w_speculative-pre-connections


- SHARE/SOCIAL

Deny Firefox Share. The Social API is an architecture that makes it easier for web browsers to integrate with social media services, using standard web technologies as the API. Once a social service provider is implemented for Firefox, it becomes possible for the browser to integrate web resources from a service, in-chrome user controls and information related to that service. For example:

a) Integration of persistent social notifications into the Firefox toolbar.

b) Integration of news feeds, tickers, buddy lists, etc., into a Firefox sidebar.

c) Integration of chat, voice, video, etc. into docked or floating window.

d) Integration of a share/recommend service in the Firefox toolbar.

You must disable it:

    social.shareDirectory=
    social.directories=
    social.whitelist=
    social.remote-install.enabled=false
    social.share.activationPanelEnabled=false
    social.toast-notifications.enabled=false

https://wiki.mozilla.org/Firefox_Social_Integration


- CAST/CAPTURE/SCREENSHARING

Deny WebRTC WG (videocapturing and translation) and Media Capture Task Force 

    media.getusermedia.browser.enabled=false
    media.getusermedia.screensharing.enabled=false
    media.getusermedia.screensharing.allowed_domains=

https://wiki.mozilla.org/Media/getUserMedia

Block "Send Video To Device". Firefox contains a "Send Video To Device" feature to send HTML5 video content to a Roku, Chromecast or similar device in the same network. In order to discover and pair with such a device, Firefox will send SSDP packages to the local network. Switch to:

    browser.casting.enabled=false (Android only)

https://support.mozilla.org/en-US/kb/how-stop-firefox-making-automatic-connections


- DRM (Encrypted Media Extensions, EME)

Deny DRM (closed-source). Encrypted Media Extensions (EME) is a JavaScript API for playing DRMed (not free) video content in HTML. A DRM component called a Content Decryption Module (CDM) decrypts, decodes, and displays the video. Switch to:

    media.eme.enabled=false
    media.gmp-eme-adobe.enabled=false

https://wiki.mozilla.org/Media/EME


- WI-FI

Deny WI-FI leaks and Firefox debugging by WI-FI. Firefox gathers information about nearby wireless access points and your computer’s IP address. Then Firefox sends this information to the default geolocation service provider, Google Location Services, to get an estimate of your location. Switch to:

    network.tickle-wifi.enabled=false
    geo.wifi.uri=
    devtools.remote.wifi.scan=false
    devtools.remote.wifi.visible=false

http://kb.mozillazine.org/Geo.wifi.uri


- WORKERS

Deny Web Workers. This is API for running scripts in the background independently of any user interface scripts. Generally, workers are expected to be long-lived, have a high start-up performance cost, and a high per-instance memory cost. It works even page with wep-app closed by user. Switch to:

    dom.serviceWorkers.enabled=false
    dom.workers.enabled=false
    dom.workers.websocket.enabled=false

https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API/Using_Service_Workers


- HSTS

Deny HSTS tracking. The feature is enabled by default and no preference to disable it. HTTP Strict Transport Security (HSTS) is a security mechanism which helps to protect websites against protocol downgrade attacks. It allows servers to declare that browser should only interact with it using secure HTTPS. But the implementation of HSTS in browsers looks like supercookie's intrusion (using the technology that was designed to improve user security). Firefox saves HSTS information in the root of profile folder:

SiteSecurityServiceState.txt

    support.mozilla.org:HSTS	0	17849	1535470706051,1,0
    duckduckgo.com:HSTS		0	17849	1535470693691,1,0
    (...)

It's a real fingerprints of the browser!

To prevent HSTS tracking.

a) close Firefox;

b) open SiteSecurityServiceState.txt and delete all strings.

c) save and close file.

d) make this file read-only.

For example (Linux only):

    chmod 400 SiteSecurityServiceState.txt

e) check rights, it must be: 

    -r--------

https://en.wikipedia.org/wiki/HSTS

https://en.wikipedia.org/wiki/Downgrade_attack


- HARDWARE

Block hardware acceleration:

    layers.acceleration.disabled=true

https://support.mozilla.org/en-US/questions/1075336

Block sensors. The Sensor API allows to retrieve values from sensors available from the device. Switch to:

    device.sensors.enabled=false

https://wiki.mozilla.org/Sensor_API 

Block BatteryManager. This interface provides ways to get information about the system's battery charge level. Switch to:

    dom.battery.enabled=false

https://developer.mozilla.org/en-US/docs/Web/API/BatteryManager

Block vibrator. Vibration API is defined as part of the nsIDOMNavigator interface. It includes the vibrate() method to let the device vibrate or let it stop vibrating. Switch to:

    dom.vibrator.enabled=false

https://wiki.mozilla.org/B2G/QA/WebAPI_Test_Plan/Vibration

Block camera. This feature is not on a current W3C standards track, but it is supported on the Firefox OS platform. Switch to:

    media.navigator.enabled=false
    media.navigator.video.enabled=false
    camera.control.autofocus_moving_callback.enabled=false
    camera.control.face_detection.enabled=false
    device.camera.enabled=false  (Android)

https://wiki.mozilla.org/Media/getUserMedia


- INTERFACE

Block animation of browser's elements:

    browser.fullscreen.animateUp=0
    browser.tabs.animate=false
    alerts.disableSlidingEffect=true
    nglayout.enable_drag_images=false

Block "enhanced page":

    browser.newtab.url=about:blank
    browser.newtabpage.enabled=false
    browser.newtabpage.enhanced=false
    browser.newtabpage.pinned=
    browser.startup.homepage=about:blank ("пустая страница"; рекомендуется)
    startup.homepage_welcome_url=

Deny smooth scrolling for the corresponding arrowscrollbox. Switch to:

    general.smoothScroll=false

https://developer.mozilla.org/en-US/docs/Mozilla/Tech/XUL/Attribute/smoothscroll


## IV. SEARCH PLUGINS

Search plugins, which included in Firefox by default, has at least five problems:

a) as a rule (by default) - unencrypted (HTTP) connection to search server. You have a potential risk to disclose own search preferences;

b) the picture (favicon) in base64 that built-in in source code;

c) plugin *may include* the special identificator. This may decrease your anonymity;

d) search string may include additional settings and the search server may get several pieces of data to determine your operating systems, browser version, etc.:

e) autosuggestion of search results.

To prevent this risks:

a) delete ALL defaults search plugins from Firefox;

b) close browser;

c) create subfolder "searchplugins" in the current Firefox's profile;

d) download next files from our repository:

    search-duckduckgo-ssl-html.xml
    search-google-ssl.xml
    search-yandex-ssl.xml
    search-wikipedia-en-ssl.xml
    search-wikipedia-ru-ssl.xml
    search-youtube-ssl.xml

and copy files to /searchplugins

**Attention:** Please remember that Google and Yandex forever trace your search activity. Use DuckDuckGo instead.

http://www.opensearch.org/

https://developer.mozilla.org/en-US/Add-ons/Creating_OpenSearch_plugins_for_Firefox


## V. ATENTION! ANDROID/iOS

**Be very carefull!**

**Firefox for Android and Firefox for iOS: In order to understand the performance of certain Mozilla marketing campaigns, Firefox sends data, including a Google advertising ID, IP address, timestamp, country, language/locale, operating system, app version, to our third party vendor. This data allows us to attribute an install to a specific advertising channel and optimize marketing campaign strategies.**

https://www.mozilla.org/en-US/privacy/firefox/
