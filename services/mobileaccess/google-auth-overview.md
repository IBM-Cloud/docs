



<!DOCTYPE html>
<html lang="en" class=" is-copy-enabled">
  <head prefix="og: http://ogp.me/ns# fb: http://ogp.me/ns/fb# object: http://ogp.me/ns/object# article: http://ogp.me/ns/article# profile: http://ogp.me/ns/profile#">
    <meta charset='utf-8'>

    <link crossorigin="anonymous" href="https://assets-cdn.github.com/assets/frameworks-e53fc1ddbde2a9e5645df620f65c80ef723c741b33293b6f22a2b7f2c8145fcf.css" integrity="sha256-5T/B3b3iqeVkXfYg9lyA73I8dBszKTtvIqK38sgUX88=" media="all" rel="stylesheet" />
    <link crossorigin="anonymous" href="https://assets-cdn.github.com/assets/github-4664ce357daee067bd8ee8e99e0833d04b115022dbf4ca637241c0f7d1f832b7.css" integrity="sha256-RmTONX2u4Ge9jujpnggz0EsRUCLb9MpjckHA99H4Mrc=" media="all" rel="stylesheet" />
    
    
    
    

    <link as="script" href="https://assets-cdn.github.com/assets/frameworks-404cdd1add1f710db016a02e5e31fff8a9089d14ff0c227df862b780886db7d5.js" rel="preload" />
    
    <link as="script" href="https://assets-cdn.github.com/assets/github-bda6c8f3d777243f9192f7725d680673aa13394eaeee5081e53f00e42e950028.js" rel="preload" />

    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta http-equiv="Content-Language" content="en">
    <meta name="viewport" content="width=device-width">
    <meta content="origin-when-cross-origin" name="referrer" />
    
    <title>docs-staging/google-auth-overview.md at master · IBM-Bluemix/docs-staging</title>
    <link rel="search" type="application/opensearchdescription+xml" href="/opensearch.xml" title="GitHub">
    <link rel="fluid-icon" href="https://github.com/fluidicon.png" title="GitHub">
    <link rel="apple-touch-icon" href="/apple-touch-icon.png">
    <link rel="apple-touch-icon" sizes="57x57" href="/apple-touch-icon-57x57.png">
    <link rel="apple-touch-icon" sizes="60x60" href="/apple-touch-icon-60x60.png">
    <link rel="apple-touch-icon" sizes="72x72" href="/apple-touch-icon-72x72.png">
    <link rel="apple-touch-icon" sizes="76x76" href="/apple-touch-icon-76x76.png">
    <link rel="apple-touch-icon" sizes="114x114" href="/apple-touch-icon-114x114.png">
    <link rel="apple-touch-icon" sizes="120x120" href="/apple-touch-icon-120x120.png">
    <link rel="apple-touch-icon" sizes="144x144" href="/apple-touch-icon-144x144.png">
    <link rel="apple-touch-icon" sizes="152x152" href="/apple-touch-icon-152x152.png">
    <link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon-180x180.png">
    <meta property="fb:app_id" content="1401488693436528">

      <meta content="https://avatars2.githubusercontent.com/u/7284885?v=3&amp;s=400" name="twitter:image:src" /><meta content="@github" name="twitter:site" /><meta content="summary" name="twitter:card" /><meta content="IBM-Bluemix/docs-staging" name="twitter:title" /><meta content="docs-staging - IBM Bluemix documentation on the staging app." name="twitter:description" />
      <meta content="https://avatars2.githubusercontent.com/u/7284885?v=3&amp;s=400" property="og:image" /><meta content="GitHub" property="og:site_name" /><meta content="object" property="og:type" /><meta content="IBM-Bluemix/docs-staging" property="og:title" /><meta content="https://github.com/IBM-Bluemix/docs-staging" property="og:url" /><meta content="docs-staging - IBM Bluemix documentation on the staging app." property="og:description" />
      <meta name="browser-stats-url" content="https://api.github.com/_private/browser/stats">
    <meta name="browser-errors-url" content="https://api.github.com/_private/browser/errors">
    <link rel="assets" href="https://assets-cdn.github.com/">
    <link rel="web-socket" href="wss://live.github.com/_sockets/MTY4NjMwNzg6MDZhOWJkMDQwOTRiOTRhNTkyZTllYzVlNzc1NDdhZjM6YWQyZDVmYTY0NTUxZTA0MGFlMzEwNGM2OTc4YTQxYjNhMmYxMzhjMWViM2E2ZGJmNDBhNTc1MTJlZDNmMTgxNQ==--5b7724b07397ec9abae4a4bc2cab6fb8eb458827">
    <meta name="pjax-timeout" content="1000">
    <link rel="sudo-modal" href="/sessions/sudo_modal">

    <meta name="msapplication-TileImage" content="/windows-tile.png">
    <meta name="msapplication-TileColor" content="#ffffff">
    <meta name="selected-link" value="repo_source" data-pjax-transient>

    <meta name="google-site-verification" content="KT5gs8h0wvaagLKAVWq8bbeNwnZZK1r1XQysX3xurLU">
<meta name="google-site-verification" content="ZzhVyEFwb7w3e0-uOTltm8Jsck2F5StVihD0exw2fsA">
    <meta name="google-analytics" content="UA-3769691-2">

<meta content="collector.githubapp.com" name="octolytics-host" /><meta content="github" name="octolytics-app-id" /><meta content="C36E28F6:2BC5:8688D45:5790BE36" name="octolytics-dimension-request_id" /><meta content="16863078" name="octolytics-actor-id" /><meta content="jergirl" name="octolytics-actor-login" /><meta content="d11eb53b80aa964bb40a401c764876267e504da721f7d9079e2540cc373ceb97" name="octolytics-actor-hash" />
<meta content="/&lt;user-name&gt;/&lt;repo-name&gt;/blob/show" data-pjax-transient="true" name="analytics-location" />



  <meta class="js-ga-set" name="dimension1" content="Logged In">



        <meta name="hostname" content="github.com">
    <meta name="user-login" content="jergirl">

        <meta name="expected-hostname" content="github.com">
      <meta name="js-proxy-site-detection-payload" content="NDVkNTJkM2JhZDY4ZjVlYWU2ZjBhOGU0MjQ1ZDY0MzY2ODgxY2EzMDAwMzk5YjIyNDJjZjllZTEwNmEwMzQ5NHx7InJlbW90ZV9hZGRyZXNzIjoiMTk1LjExMC40MC4yNDYiLCJyZXF1ZXN0X2lkIjoiQzM2RTI4RjY6MkJDNTo4Njg4RDQ1OjU3OTBCRTM2IiwidGltZXN0YW1wIjoxNDY5MTAzNjcwfQ==">


      <link rel="mask-icon" href="https://assets-cdn.github.com/pinned-octocat.svg" color="#4078c0">
      <link rel="icon" type="image/x-icon" href="https://assets-cdn.github.com/favicon.ico">

    <meta name="html-safe-nonce" content="63c716447c96747282ba696a86a155a2d7a53e30">
    <meta content="9d725a0f2ec9cef3ada60ee7c58b904f69bd9c48" name="form-nonce" />

    <meta http-equiv="x-pjax-version" content="c85c9b6f8432cc7b07e5ce5161e4d4fc">
    

      
  <meta name="description" content="docs-staging - IBM Bluemix documentation on the staging app.">
  <meta name="go-import" content="github.com/IBM-Bluemix/docs-staging git https://github.com/IBM-Bluemix/docs-staging.git">

  <meta content="7284885" name="octolytics-dimension-user_id" /><meta content="IBM-Bluemix" name="octolytics-dimension-user_login" /><meta content="39894162" name="octolytics-dimension-repository_id" /><meta content="IBM-Bluemix/docs-staging" name="octolytics-dimension-repository_nwo" /><meta content="false" name="octolytics-dimension-repository_public" /><meta content="false" name="octolytics-dimension-repository_is_fork" /><meta content="39894162" name="octolytics-dimension-repository_network_root_id" /><meta content="IBM-Bluemix/docs-staging" name="octolytics-dimension-repository_network_root_nwo" />
  <link href="https://github.com/IBM-Bluemix/docs-staging/commits/master.atom?token=AQFPZixLkO56Z5ViRv1Nmk_Ub_85E2gAks61nK1GwA%3D%3D" rel="alternate" title="Recent Commits to docs-staging:master" type="application/atom+xml">


      <link rel="canonical" href="https://github.com/IBM-Bluemix/docs-staging/blob/master/services/mobileaccess/google-auth-overview.md" data-pjax-transient>
  </head>


  <body class="logged-in   env-production windows vis-private page-blob">
    <div id="js-pjax-loader-bar" class="pjax-loader-bar"></div>
    <a href="#start-of-content" tabindex="1" class="accessibility-aid js-skip-to-content">Skip to content</a>

    
    
    



        <div class="header header-logged-in true" role="banner">
  <div class="container clearfix">

    <a class="header-logo-invertocat" href="https://github.com/" data-hotkey="g d" aria-label="Homepage" data-ga-click="Header, go to dashboard, icon:logo">
  <svg aria-hidden="true" class="octicon octicon-mark-github" height="28" version="1.1" viewBox="0 0 16 16" width="28"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0 0 16 8c0-4.42-3.58-8-8-8z"></path></svg>
</a>


        <div class="header-search scoped-search site-scoped-search js-site-search" role="search">
  <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/IBM-Bluemix/docs-staging/search" class="js-site-search-form" data-scoped-search-url="/IBM-Bluemix/docs-staging/search" data-unscoped-search-url="/search" method="get"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /></div>
    <label class="form-control header-search-wrapper js-chromeless-input-container">
      <div class="header-search-scope">This repository</div>
      <input type="text"
        class="form-control header-search-input js-site-search-focus js-site-search-field is-clearable"
        data-hotkey="s"
        name="q"
        placeholder="Search"
        aria-label="Search this repository"
        data-unscoped-placeholder="Search GitHub"
        data-scoped-placeholder="Search"
        tabindex="1"
        autocapitalize="off">
    </label>
</form></div>


      <ul class="header-nav left" role="navigation">
        <li class="header-nav-item">
          <a href="/pulls" class="js-selected-navigation-item header-nav-link" data-ga-click="Header, click, Nav menu - item:pulls context:user" data-hotkey="g p" data-selected-links="/pulls /pulls/assigned /pulls/mentioned /pulls">
            Pull requests
</a>        </li>
        <li class="header-nav-item">
          <a href="/issues" class="js-selected-navigation-item header-nav-link" data-ga-click="Header, click, Nav menu - item:issues context:user" data-hotkey="g i" data-selected-links="/issues /issues/assigned /issues/mentioned /issues">
            Issues
</a>        </li>
          <li class="header-nav-item">
            <a class="header-nav-link" href="https://gist.github.com/" data-ga-click="Header, go to gist, text:gist">Gist</a>
          </li>
      </ul>

    
<ul class="header-nav user-nav right" id="user-links">
  <li class="header-nav-item">
    

  </li>

  <li class="header-nav-item dropdown js-menu-container">
    <a class="header-nav-link tooltipped tooltipped-s js-menu-target" href="/new"
       aria-label="Create new…"
       data-ga-click="Header, create new, icon:add">
      <svg aria-hidden="true" class="octicon octicon-plus left" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 9H7v5H5V9H0V7h5V2h2v5h5z"></path></svg>
      <span class="dropdown-caret"></span>
    </a>

    <div class="dropdown-menu-content js-menu-content">
      <ul class="dropdown-menu dropdown-menu-sw">
        
<a class="dropdown-item" href="/new" data-ga-click="Header, create new repository">
  New repository
</a>

  <a class="dropdown-item" href="/new/import" data-ga-click="Header, import a repository">
    Import repository
  </a>


  <a class="dropdown-item" href="/organizations/new" data-ga-click="Header, create new organization">
    New organization
  </a>



  <div class="dropdown-divider"></div>
  <div class="dropdown-header">
    <span title="IBM-Bluemix/docs-staging">This repository</span>
  </div>
    <a class="dropdown-item" href="/IBM-Bluemix/docs-staging/issues/new" data-ga-click="Header, create new issue">
      New issue
    </a>

      </ul>
    </div>
  </li>

  <li class="header-nav-item dropdown js-menu-container">
    <a class="header-nav-link name tooltipped tooltipped-sw js-menu-target" href="/jergirl"
       aria-label="View profile and more"
       data-ga-click="Header, show menu, icon:avatar">
      <img alt="@jergirl" class="avatar" height="20" src="https://avatars1.githubusercontent.com/u/16863078?v=3&amp;s=40" width="20" />
      <span class="dropdown-caret"></span>
    </a>

    <div class="dropdown-menu-content js-menu-content">
      <div class="dropdown-menu dropdown-menu-sw">
        <div class="dropdown-header header-nav-current-user css-truncate">
          Signed in as <strong class="css-truncate-target">jergirl</strong>
        </div>

        <div class="dropdown-divider"></div>

        <a class="dropdown-item" href="/jergirl" data-ga-click="Header, go to profile, text:your profile">
          Your profile
        </a>
        <a class="dropdown-item" href="/stars" data-ga-click="Header, go to starred repos, text:your stars">
          Your stars
        </a>
        <a class="dropdown-item" href="/explore" data-ga-click="Header, go to explore, text:explore">
          Explore
        </a>
          <a class="dropdown-item" href="/integrations" data-ga-click="Header, go to integrations, text:integrations">
            Integrations
          </a>
        <a class="dropdown-item" href="https://help.github.com" data-ga-click="Header, go to help, text:help">
          Help
        </a>


        <div class="dropdown-divider"></div>

        <a class="dropdown-item" href="/settings/profile" data-ga-click="Header, go to settings, icon:settings">
          Settings
        </a>

        <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/logout" class="logout-form" data-form-nonce="9d725a0f2ec9cef3ada60ee7c58b904f69bd9c48" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="V2dpinZPshIrgzY+6dYOTq0zy0Cdj7CoIu3e3d4iaFQJnkkcY1uRTr/NOHFPKzWa9TLZOK7swdvrdhsL1dxOVw==" /></div>
          <button class="dropdown-item dropdown-signout" data-ga-click="Header, sign out, icon:logout">
            Sign out
          </button>
</form>      </div>
    </div>
  </li>
</ul>


    
  </div>
</div>


      


    <div id="start-of-content" class="accessibility-aid"></div>

      <div id="js-flash-container">
</div>


    <div role="main">
        <div itemscope itemtype="http://schema.org/SoftwareSourceCode">
    <div id="js-repo-pjax-container" data-pjax-container>
      
<div class="pagehead repohead instapaper_ignore readability-menu experiment-repo-nav">
  <div class="container repohead-details-container">

    

<ul class="pagehead-actions">

  <li>
        <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/notifications/subscribe" class="js-social-container" data-autosubmit="true" data-form-nonce="9d725a0f2ec9cef3ada60ee7c58b904f69bd9c48" data-remote="true" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="0szT8jz2BShjjoVduzUruRNNmerMXXNGwB8OH0EYkKaG4CuVgjcPKW5QiiRatMdc3iFJyFoHyyXcnmaOjGH4Vg==" /></div>      <input class="form-control" id="repository_id" name="repository_id" type="hidden" value="39894162" />

        <div class="select-menu js-menu-container js-select-menu">
          <a href="/IBM-Bluemix/docs-staging/subscription"
            class="btn btn-sm btn-with-count select-menu-button js-menu-target" role="button" tabindex="0" aria-haspopup="true"
            data-ga-click="Repository, click Watch settings, action:blob#show">
            <span class="js-select-button">
              <svg aria-hidden="true" class="octicon octicon-eye" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M8.06 2C3 2 0 8 0 8s3 6 8.06 6C13 14 16 8 16 8s-3-6-7.94-6zM8 12c-2.2 0-4-1.78-4-4 0-2.2 1.8-4 4-4 2.22 0 4 1.8 4 4 0 2.22-1.78 4-4 4zm2-4c0 1.11-.89 2-2 2-1.11 0-2-.89-2-2 0-1.11.89-2 2-2 1.11 0 2 .89 2 2z"></path></svg>
              Unwatch
            </span>
          </a>
          <a class="social-count js-social-count" href="/IBM-Bluemix/docs-staging/watchers">
            66
          </a>

        <div class="select-menu-modal-holder">
          <div class="select-menu-modal subscription-menu-modal js-menu-content" aria-hidden="true">
            <div class="select-menu-header js-navigation-enable" tabindex="-1">
              <svg aria-label="Close" class="octicon octicon-x js-menu-close" height="16" role="img" version="1.1" viewBox="0 0 12 16" width="12"><path d="M7.48 8l3.75 3.75-1.48 1.48L6 9.48l-3.75 3.75-1.48-1.48L4.52 8 .77 4.25l1.48-1.48L6 6.52l3.75-3.75 1.48 1.48z"></path></svg>
              <span class="select-menu-title">Notifications</span>
            </div>

              <div class="select-menu-list js-navigation-container" role="menu">

                <div class="select-menu-item js-navigation-item " role="menuitem" tabindex="0">
                  <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
                  <div class="select-menu-item-text">
                    <input id="do_included" name="do" type="radio" value="included" />
                    <span class="select-menu-item-heading">Not watching</span>
                    <span class="description">Be notified when participating or @mentioned.</span>
                    <span class="js-select-button-text hidden-select-button-text">
                      <svg aria-hidden="true" class="octicon octicon-eye" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M8.06 2C3 2 0 8 0 8s3 6 8.06 6C13 14 16 8 16 8s-3-6-7.94-6zM8 12c-2.2 0-4-1.78-4-4 0-2.2 1.8-4 4-4 2.22 0 4 1.8 4 4 0 2.22-1.78 4-4 4zm2-4c0 1.11-.89 2-2 2-1.11 0-2-.89-2-2 0-1.11.89-2 2-2 1.11 0 2 .89 2 2z"></path></svg>
                      Watch
                    </span>
                  </div>
                </div>

                <div class="select-menu-item js-navigation-item selected" role="menuitem" tabindex="0">
                  <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
                  <div class="select-menu-item-text">
                    <input checked="checked" id="do_subscribed" name="do" type="radio" value="subscribed" />
                    <span class="select-menu-item-heading">Watching</span>
                    <span class="description">Be notified of all conversations.</span>
                    <span class="js-select-button-text hidden-select-button-text">
                      <svg aria-hidden="true" class="octicon octicon-eye" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M8.06 2C3 2 0 8 0 8s3 6 8.06 6C13 14 16 8 16 8s-3-6-7.94-6zM8 12c-2.2 0-4-1.78-4-4 0-2.2 1.8-4 4-4 2.22 0 4 1.8 4 4 0 2.22-1.78 4-4 4zm2-4c0 1.11-.89 2-2 2-1.11 0-2-.89-2-2 0-1.11.89-2 2-2 1.11 0 2 .89 2 2z"></path></svg>
                      Unwatch
                    </span>
                  </div>
                </div>

                <div class="select-menu-item js-navigation-item " role="menuitem" tabindex="0">
                  <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
                  <div class="select-menu-item-text">
                    <input id="do_ignore" name="do" type="radio" value="ignore" />
                    <span class="select-menu-item-heading">Ignoring</span>
                    <span class="description">Never be notified.</span>
                    <span class="js-select-button-text hidden-select-button-text">
                      <svg aria-hidden="true" class="octicon octicon-mute" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M8 2.81v10.38c0 .67-.81 1-1.28.53L3 10H1c-.55 0-1-.45-1-1V7c0-.55.45-1 1-1h2l3.72-3.72C7.19 1.81 8 2.14 8 2.81zm7.53 3.22l-1.06-1.06-1.97 1.97-1.97-1.97-1.06 1.06L11.44 8 9.47 9.97l1.06 1.06 1.97-1.97 1.97 1.97 1.06-1.06L13.56 8l1.97-1.97z"></path></svg>
                      Stop ignoring
                    </span>
                  </div>
                </div>

              </div>

            </div>
          </div>
        </div>
</form>
  </li>

  <li>
    
  <div class="js-toggler-container js-social-container starring-container ">

    <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/IBM-Bluemix/docs-staging/unstar" class="starred" data-form-nonce="9d725a0f2ec9cef3ada60ee7c58b904f69bd9c48" data-remote="true" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="DDsY/MRxPYwyscHBt+90txYP1lfmU5x4M2UHOrcafDnClLlfJPwrNoTEMwUdZfbrads0Gy35bwrrv0dmPcinlg==" /></div>
      <button
        class="btn btn-sm btn-with-count js-toggler-target"
        aria-label="Unstar this repository" title="Unstar IBM-Bluemix/docs-staging"
        data-ga-click="Repository, click unstar button, action:blob#show; text:Unstar">
        <svg aria-hidden="true" class="octicon octicon-star" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path d="M14 6l-4.9-.64L7 1 4.9 5.36 0 6l3.6 3.26L2.67 14 7 11.67 11.33 14l-.93-4.74z"></path></svg>
        Unstar
      </button>
        <a class="social-count js-social-count" href="/IBM-Bluemix/docs-staging/stargazers">
          4
        </a>
</form>
    <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/IBM-Bluemix/docs-staging/star" class="unstarred" data-form-nonce="9d725a0f2ec9cef3ada60ee7c58b904f69bd9c48" data-remote="true" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="/iypQCSqKwTOR4JaJF5Z10SwVSc6HSds/vm2mwoCHsKW2HyqRbCD5R31AtiJd8TEza0eiN01GYSfXQ5jjRr75A==" /></div>
      <button
        class="btn btn-sm btn-with-count js-toggler-target"
        aria-label="Star this repository" title="Star IBM-Bluemix/docs-staging"
        data-ga-click="Repository, click star button, action:blob#show; text:Star">
        <svg aria-hidden="true" class="octicon octicon-star" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path d="M14 6l-4.9-.64L7 1 4.9 5.36 0 6l3.6 3.26L2.67 14 7 11.67 11.33 14l-.93-4.74z"></path></svg>
        Star
      </button>
        <a class="social-count js-social-count" href="/IBM-Bluemix/docs-staging/stargazers">
          4
        </a>
</form>  </div>

  </li>

  <li>
          <a href="#fork-destination-box" class="btn btn-sm btn-with-count"
              title="Fork your own copy of IBM-Bluemix/docs-staging to your account"
              aria-label="Fork your own copy of IBM-Bluemix/docs-staging to your account"
              rel="facebox"
              data-ga-click="Repository, show fork modal, action:blob#show; text:Fork">
              <svg aria-hidden="true" class="octicon octicon-repo-forked" height="16" version="1.1" viewBox="0 0 10 16" width="10"><path d="M8 1a1.993 1.993 0 0 0-1 3.72V6L5 8 3 6V4.72A1.993 1.993 0 0 0 2 1a1.993 1.993 0 0 0-1 3.72V6.5l3 3v1.78A1.993 1.993 0 0 0 5 15a1.993 1.993 0 0 0 1-3.72V9.5l3-3V4.72A1.993 1.993 0 0 0 8 1zM2 4.2C1.34 4.2.8 3.65.8 3c0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2zm3 10c-.66 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2zm3-10c-.66 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2z"></path></svg>
            Fork
          </a>

          <div id="fork-destination-box" style="display: none;">
            <h2 class="facebox-header" data-facebox-id="facebox-header">Where should we fork this repository?</h2>
            <include-fragment src=""
                class="js-fork-select-fragment fork-select-fragment"
                data-url="/IBM-Bluemix/docs-staging/fork?fragment=1">
              <img alt="Loading" height="64" src="https://assets-cdn.github.com/images/spinners/octocat-spinner-128.gif" width="64" />
            </include-fragment>
          </div>

    <a href="/IBM-Bluemix/docs-staging/network" class="social-count">
      39
    </a>
  </li>
</ul>

    <h1 class="private ">
  <svg aria-hidden="true" class="octicon octicon-lock" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M4 13H3v-1h1v1zm8-6v7c0 .55-.45 1-1 1H1c-.55 0-1-.45-1-1V7c0-.55.45-1 1-1h1V4c0-2.2 1.8-4 4-4s4 1.8 4 4v2h1c.55 0 1 .45 1 1zM3.8 6h4.41V4c0-1.22-.98-2.2-2.2-2.2-1.22 0-2.2.98-2.2 2.2v2H3.8zM11 7H2v7h9V7zM4 8H3v1h1V8zm0 2H3v1h1v-1z"></path></svg>
  <span class="author" itemprop="author"><a href="/IBM-Bluemix" class="url fn" rel="author">IBM-Bluemix</a></span><!--
--><span class="path-divider">/</span><!--
--><strong itemprop="name"><a href="/IBM-Bluemix/docs-staging" data-pjax="#js-repo-pjax-container">docs-staging</a></strong>
    <span class="label label-private v-align-middle">Private</span>

</h1>

  </div>
  <div class="container">
    
<nav class="reponav js-repo-nav js-sidenav-container-pjax"
     itemscope
     itemtype="http://schema.org/BreadcrumbList"
     role="navigation"
     data-pjax="#js-repo-pjax-container">

  <span itemscope itemtype="http://schema.org/ListItem" itemprop="itemListElement">
    <a href="/IBM-Bluemix/docs-staging" aria-selected="true" class="js-selected-navigation-item selected reponav-item" data-hotkey="g c" data-selected-links="repo_source repo_downloads repo_commits repo_releases repo_tags repo_branches /IBM-Bluemix/docs-staging" itemprop="url">
      <svg aria-hidden="true" class="octicon octicon-code" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path d="M9.5 3L8 4.5 11.5 8 8 11.5 9.5 13 14 8 9.5 3zm-5 0L0 8l4.5 5L6 11.5 2.5 8 6 4.5 4.5 3z"></path></svg>
      <span itemprop="name">Code</span>
      <meta itemprop="position" content="1">
</a>  </span>

    <span itemscope itemtype="http://schema.org/ListItem" itemprop="itemListElement">
      <a href="/IBM-Bluemix/docs-staging/issues" class="js-selected-navigation-item reponav-item" data-hotkey="g i" data-selected-links="repo_issues repo_labels repo_milestones /IBM-Bluemix/docs-staging/issues" itemprop="url">
        <svg aria-hidden="true" class="octicon octicon-issue-opened" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path d="M7 2.3c3.14 0 5.7 2.56 5.7 5.7s-2.56 5.7-5.7 5.7A5.71 5.71 0 0 1 1.3 8c0-3.14 2.56-5.7 5.7-5.7zM7 1C3.14 1 0 4.14 0 8s3.14 7 7 7 7-3.14 7-7-3.14-7-7-7zm1 3H6v5h2V4zm0 6H6v2h2v-2z"></path></svg>
        <span itemprop="name">Issues</span>
        <span class="counter">1</span>
        <meta itemprop="position" content="2">
</a>    </span>

  <span itemscope itemtype="http://schema.org/ListItem" itemprop="itemListElement">
    <a href="/IBM-Bluemix/docs-staging/pulls" class="js-selected-navigation-item reponav-item" data-hotkey="g p" data-selected-links="repo_pulls /IBM-Bluemix/docs-staging/pulls" itemprop="url">
      <svg aria-hidden="true" class="octicon octicon-git-pull-request" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M11 11.28V5c-.03-.78-.34-1.47-.94-2.06C9.46 2.35 8.78 2.03 8 2H7V0L4 3l3 3V4h1c.27.02.48.11.69.31.21.2.3.42.31.69v6.28A1.993 1.993 0 0 0 10 15a1.993 1.993 0 0 0 1-3.72zm-1 2.92c-.66 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2zM4 3c0-1.11-.89-2-2-2a1.993 1.993 0 0 0-1 3.72v6.56A1.993 1.993 0 0 0 2 15a1.993 1.993 0 0 0 1-3.72V4.72c.59-.34 1-.98 1-1.72zm-.8 10c0 .66-.55 1.2-1.2 1.2-.65 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2zM2 4.2C1.34 4.2.8 3.65.8 3c0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2z"></path></svg>
      <span itemprop="name">Pull requests</span>
      <span class="counter">13</span>
      <meta itemprop="position" content="3">
</a>  </span>

    <a href="/IBM-Bluemix/docs-staging/wiki" class="js-selected-navigation-item reponav-item" data-hotkey="g w" data-selected-links="repo_wiki /IBM-Bluemix/docs-staging/wiki">
      <svg aria-hidden="true" class="octicon octicon-book" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M3 5h4v1H3V5zm0 3h4V7H3v1zm0 2h4V9H3v1zm11-5h-4v1h4V5zm0 2h-4v1h4V7zm0 2h-4v1h4V9zm2-6v9c0 .55-.45 1-1 1H9.5l-1 1-1-1H2c-.55 0-1-.45-1-1V3c0-.55.45-1 1-1h5.5l1 1 1-1H15c.55 0 1 .45 1 1zm-8 .5L7.5 3H2v9h6V3.5zm7-.5H9.5l-.5.5V12h6V3z"></path></svg>
      Wiki
</a>

  <a href="/IBM-Bluemix/docs-staging/pulse" class="js-selected-navigation-item reponav-item" data-selected-links="pulse /IBM-Bluemix/docs-staging/pulse">
    <svg aria-hidden="true" class="octicon octicon-pulse" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path d="M11.5 8L8.8 5.4 6.6 8.5 5.5 1.6 2.38 8H0v2h3.6l.9-1.8.9 5.4L9 8.5l1.6 1.5H14V8z"></path></svg>
    Pulse
</a>
  <a href="/IBM-Bluemix/docs-staging/graphs" class="js-selected-navigation-item reponav-item" data-selected-links="repo_graphs repo_contributors /IBM-Bluemix/docs-staging/graphs">
    <svg aria-hidden="true" class="octicon octicon-graph" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M16 14v1H0V0h1v14h15zM5 13H3V8h2v5zm4 0H7V3h2v10zm4 0h-2V6h2v7z"></path></svg>
    Graphs
</a>

</nav>

  </div>
</div>

<div class="container new-discussion-timeline experiment-repo-nav">
  <div class="repository-content">

    

<a href="/IBM-Bluemix/docs-staging/blob/a28236bc9b6b9d372219f671f7db045e4b35d8ae/services/mobileaccess/google-auth-overview.md" class="hidden js-permalink-shortcut" data-hotkey="y">Permalink</a>

<!-- blob contrib key: blob_contributors:v21:46a2b4e87eeb6631700603d51efff1c9 -->

<div class="file-navigation js-zeroclipboard-container">
  
<div class="select-menu branch-select-menu js-menu-container js-select-menu left">
  <button class="btn btn-sm select-menu-button js-menu-target css-truncate" data-hotkey="w"
    title="master"
    type="button" aria-label="Switch branches or tags" tabindex="0" aria-haspopup="true">
    <i>Branch:</i>
    <span class="js-select-button css-truncate-target">master</span>
  </button>

  <div class="select-menu-modal-holder js-menu-content js-navigation-container" data-pjax aria-hidden="true">

    <div class="select-menu-modal">
      <div class="select-menu-header">
        <svg aria-label="Close" class="octicon octicon-x js-menu-close" height="16" role="img" version="1.1" viewBox="0 0 12 16" width="12"><path d="M7.48 8l3.75 3.75-1.48 1.48L6 9.48l-3.75 3.75-1.48-1.48L4.52 8 .77 4.25l1.48-1.48L6 6.52l3.75-3.75 1.48 1.48z"></path></svg>
        <span class="select-menu-title">Switch branches/tags</span>
      </div>

      <div class="select-menu-filters">
        <div class="select-menu-text-filter">
          <input type="text" aria-label="Find or create a branch…" id="context-commitish-filter-field" class="form-control js-filterable-field js-navigation-enable" placeholder="Find or create a branch…">
        </div>
        <div class="select-menu-tabs">
          <ul>
            <li class="select-menu-tab">
              <a href="#" data-tab-filter="branches" data-filter-placeholder="Find or create a branch…" class="js-select-menu-tab" role="tab">Branches</a>
            </li>
            <li class="select-menu-tab">
              <a href="#" data-tab-filter="tags" data-filter-placeholder="Find a tag…" class="js-select-menu-tab" role="tab">Tags</a>
            </li>
          </ul>
        </div>
      </div>

      <div class="select-menu-list select-menu-tab-bucket js-select-menu-tab-bucket" data-tab-filter="branches" role="menu">

        <div data-filterable-for="context-commitish-filter-field" data-filterable-type="substring">


            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/148440-update-docs-to-reflect-removal-of-V1-APIs-/services/mobileaccess/google-auth-overview.md"
               data-name="148440-update-docs-to-reflect-removal-of-V1-APIs-"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="148440-update-docs-to-reflect-removal-of-V1-APIs-">
                148440-update-docs-to-reflect-removal-of-V1-APIs-
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/201357-cfapps-runtimes-viewdocs/services/mobileaccess/google-auth-overview.md"
               data-name="201357-cfapps-runtimes-viewdocs"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="201357-cfapps-runtimes-viewdocs">
                201357-cfapps-runtimes-viewdocs
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/204629-starters-to-runtimes/services/mobileaccess/google-auth-overview.md"
               data-name="204629-starters-to-runtimes"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="204629-starters-to-runtimes">
                204629-starters-to-runtimes
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/212031-cfapps-runtimes/services/mobileaccess/google-auth-overview.md"
               data-name="212031-cfapps-runtimes"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="212031-cfapps-runtimes">
                212031-cfapps-runtimes
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/212368-addressedViolationInCodeBlockForLiberty/services/mobileaccess/google-auth-overview.md"
               data-name="212368-addressedViolationInCodeBlockForLiberty"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="212368-addressedViolationInCodeBlockForLiberty">
                212368-addressedViolationInCodeBlockForLiberty
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/213742-removeNewlines/services/mobileaccess/google-auth-overview.md"
               data-name="213742-removeNewlines"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="213742-removeNewlines">
                213742-removeNewlines
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/218761-link-proxy/services/mobileaccess/google-auth-overview.md"
               data-name="218761-link-proxy"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="218761-link-proxy">
                218761-link-proxy
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/218862-RemoveBulletForPsirt/services/mobileaccess/google-auth-overview.md"
               data-name="218862-RemoveBulletForPsirt"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="218862-RemoveBulletForPsirt">
                218862-RemoveBulletForPsirt
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/218862-latestUpdate-v9/services/mobileaccess/google-auth-overview.md"
               data-name="218862-latestUpdate-v9"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="218862-latestUpdate-v9">
                218862-latestUpdate-v9
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Caroline-July-work/services/mobileaccess/google-auth-overview.md"
               data-name="Caroline-July-work"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="Caroline-July-work">
                Caroline-July-work
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Creation-of-IoT-for-Automotive-Getting-Started-docs/services/mobileaccess/google-auth-overview.md"
               data-name="Creation-of-IoT-for-Automotive-Getting-Started-docs"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="Creation-of-IoT-for-Automotive-Getting-Started-docs">
                Creation-of-IoT-for-Automotive-Getting-Started-docs
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Crystal4545-patch-1/services/mobileaccess/google-auth-overview.md"
               data-name="Crystal4545-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="Crystal4545-patch-1">
                Crystal4545-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Crystal4545-patch-2/services/mobileaccess/google-auth-overview.md"
               data-name="Crystal4545-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="Crystal4545-patch-2">
                Crystal4545-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Crystal4545-patch-3/services/mobileaccess/google-auth-overview.md"
               data-name="Crystal4545-patch-3"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="Crystal4545-patch-3">
                Crystal4545-patch-3
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Crystal4545/services/mobileaccess/google-auth-overview.md"
               data-name="Crystal4545"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="Crystal4545">
                Crystal4545
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/ID-edits-to-Driver-Behaviour-overview-docs/services/mobileaccess/google-auth-overview.md"
               data-name="ID-edits-to-Driver-Behaviour-overview-docs"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="ID-edits-to-Driver-Behaviour-overview-docs">
                ID-edits-to-Driver-Behaviour-overview-docs
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/ID-edits-to-Map-insights-docs/services/mobileaccess/google-auth-overview.md"
               data-name="ID-edits-to-Map-insights-docs"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="ID-edits-to-Map-insights-docs">
                ID-edits-to-Map-insights-docs
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/MPurcell-ID-editing-and-technical-updates-to-Blockchain-contracts-docs/services/mobileaccess/google-auth-overview.md"
               data-name="MPurcell-ID-editing-and-technical-updates-to-Blockchain-contracts-docs"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="MPurcell-ID-editing-and-technical-updates-to-Blockchain-contracts-docs">
                MPurcell-ID-editing-and-technical-updates-to-Blockchain-contracts-docs
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Sec-bluemix-ed/services/mobileaccess/google-auth-overview.md"
               data-name="Sec-bluemix-ed"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="Sec-bluemix-ed">
                Sec-bluemix-ed
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Updates-and-edits-to-new-Driver-Behavior-admin-feature/services/mobileaccess/google-auth-overview.md"
               data-name="Updates-and-edits-to-new-Driver-Behavior-admin-feature"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="Updates-and-edits-to-new-Driver-Behavior-admin-feature">
                Updates-and-edits-to-new-Driver-Behavior-admin-feature
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/automotive-ID-review/services/mobileaccess/google-auth-overview.md"
               data-name="automotive-ID-review"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="automotive-ID-review">
                automotive-ID-review
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/benbakowski-patch-2/services/mobileaccess/google-auth-overview.md"
               data-name="benbakowski-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="benbakowski-patch-2">
                benbakowski-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/bhpratt-patch-1/services/mobileaccess/google-auth-overview.md"
               data-name="bhpratt-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="bhpratt-patch-1">
                bhpratt-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/bhpratt-patch-2/services/mobileaccess/google-auth-overview.md"
               data-name="bhpratt-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="bhpratt-patch-2">
                bhpratt-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/bwentwor-patch-1/services/mobileaccess/google-auth-overview.md"
               data-name="bwentwor-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="bwentwor-patch-1">
                bwentwor-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/danawilson-patch-1/services/mobileaccess/google-auth-overview.md"
               data-name="danawilson-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="danawilson-patch-1">
                danawilson-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/fix_limits_table/services/mobileaccess/google-auth-overview.md"
               data-name="fix_limits_table"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="fix_limits_table">
                fix_limits_table
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/fixMyIssue/services/mobileaccess/google-auth-overview.md"
               data-name="fixMyIssue"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="fixMyIssue">
                fixMyIssue
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/gcatasta-patternengine/services/mobileaccess/google-auth-overview.md"
               data-name="gcatasta-patternengine"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="gcatasta-patternengine">
                gcatasta-patternengine
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/gshgui-patch-1/services/mobileaccess/google-auth-overview.md"
               data-name="gshgui-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="gshgui-patch-1">
                gshgui-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/iot-edge-analytics-addition/services/mobileaccess/google-auth-overview.md"
               data-name="iot-edge-analytics-addition"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="iot-edge-analytics-addition">
                iot-edge-analytics-addition
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/iot-initial/services/mobileaccess/google-auth-overview.md"
               data-name="iot-initial"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="iot-initial">
                iot-initial
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/iot-nav-changes/services/mobileaccess/google-auth-overview.md"
               data-name="iot-nav-changes"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="iot-nav-changes">
                iot-nav-changes
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/iot-platform-blockchain-merger/services/mobileaccess/google-auth-overview.md"
               data-name="iot-platform-blockchain-merger"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="iot-platform-blockchain-merger">
                iot-platform-blockchain-merger
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/iot-platform-security-iso/services/mobileaccess/google-auth-overview.md"
               data-name="iot-platform-security-iso"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="iot-platform-security-iso">
                iot-platform-security-iso
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/it8-changes/services/mobileaccess/google-auth-overview.md"
               data-name="it8-changes"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="it8-changes">
                it8-changes
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/it9-changes/services/mobileaccess/google-auth-overview.md"
               data-name="it9-changes"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="it9-changes">
                it9-changes
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jbetht-patch-1/services/mobileaccess/google-auth-overview.md"
               data-name="jbetht-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="jbetht-patch-1">
                jbetht-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jbetht-patch-2-1/services/mobileaccess/google-auth-overview.md"
               data-name="jbetht-patch-2-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="jbetht-patch-2-1">
                jbetht-patch-2-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jbetht-patch-2/services/mobileaccess/google-auth-overview.md"
               data-name="jbetht-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="jbetht-patch-2">
                jbetht-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jbetht-patch-3/services/mobileaccess/google-auth-overview.md"
               data-name="jbetht-patch-3"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="jbetht-patch-3">
                jbetht-patch-3
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jbetht-patch-8/services/mobileaccess/google-auth-overview.md"
               data-name="jbetht-patch-8"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="jbetht-patch-8">
                jbetht-patch-8
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jeffchi-patch-1/services/mobileaccess/google-auth-overview.md"
               data-name="jeffchi-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="jeffchi-patch-1">
                jeffchi-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jgchan-merge-staging-to-production/services/mobileaccess/google-auth-overview.md"
               data-name="jgchan-merge-staging-to-production"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="jgchan-merge-staging-to-production">
                jgchan-merge-staging-to-production
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jsg-branch/services/mobileaccess/google-auth-overview.md"
               data-name="jsg-branch"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="jsg-branch">
                jsg-branch
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jsg-can-patch-1/services/mobileaccess/google-auth-overview.md"
               data-name="jsg-can-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="jsg-can-patch-1">
                jsg-can-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/kKronstainBrown-patch-1/services/mobileaccess/google-auth-overview.md"
               data-name="kKronstainBrown-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="kKronstainBrown-patch-1">
                kKronstainBrown-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/kKronstainBrown-patch-2/services/mobileaccess/google-auth-overview.md"
               data-name="kKronstainBrown-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="kKronstainBrown-patch-2">
                kKronstainBrown-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/knlyons/services/mobileaccess/google-auth-overview.md"
               data-name="knlyons"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="knlyons">
                knlyons
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/last_minute_rules_action_changes/services/mobileaccess/google-auth-overview.md"
               data-name="last_minute_rules_action_changes"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="last_minute_rules_action_changes">
                last_minute_rules_action_changes
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/lopezdsr-patch-1/services/mobileaccess/google-auth-overview.md"
               data-name="lopezdsr-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="lopezdsr-patch-1">
                lopezdsr-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/lopezdsr-patch-3/services/mobileaccess/google-auth-overview.md"
               data-name="lopezdsr-patch-3"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="lopezdsr-patch-3">
                lopezdsr-patch-3
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open selected"
               href="/IBM-Bluemix/docs-staging/blob/master/services/mobileaccess/google-auth-overview.md"
               data-name="master"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="master">
                master
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/mdb-DRA-jenkins/services/mobileaccess/google-auth-overview.md"
               data-name="mdb-DRA-jenkins"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="mdb-DRA-jenkins">
                mdb-DRA-jenkins
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/mekaufman-patch-1/services/mobileaccess/google-auth-overview.md"
               data-name="mekaufman-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="mekaufman-patch-1">
                mekaufman-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/mpurcell-edits-to-improve-python-docs/services/mobileaccess/google-auth-overview.md"
               data-name="mpurcell-edits-to-improve-python-docs"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="mpurcell-edits-to-improve-python-docs">
                mpurcell-edits-to-improve-python-docs
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/mpurcell-new-client-connection-topic/services/mobileaccess/google-auth-overview.md"
               data-name="mpurcell-new-client-connection-topic"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="mpurcell-new-client-connection-topic">
                mpurcell-new-client-connection-topic
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/mpurcell-technical-dev-doc-edits-for-GA-release/services/mobileaccess/google-auth-overview.md"
               data-name="mpurcell-technical-dev-doc-edits-for-GA-release"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="mpurcell-technical-dev-doc-edits-for-GA-release">
                mpurcell-technical-dev-doc-edits-for-GA-release
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/mpurcell-updates-to-automotive-services-for-release-refreshes-22nd-july/services/mobileaccess/google-auth-overview.md"
               data-name="mpurcell-updates-to-automotive-services-for-release-refreshes-22nd-july"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="mpurcell-updates-to-automotive-services-for-release-refreshes-22nd-july">
                mpurcell-updates-to-automotive-services-for-release-refreshes-22nd-july
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/offlinemode/services/mobileaccess/google-auth-overview.md"
               data-name="offlinemode"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="offlinemode">
                offlinemode
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/pr/481/services/mobileaccess/google-auth-overview.md"
               data-name="pr/481"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="pr/481">
                pr/481
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/pr/661/services/mobileaccess/google-auth-overview.md"
               data-name="pr/661"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="pr/661">
                pr/661
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/pr/903/services/mobileaccess/google-auth-overview.md"
               data-name="pr/903"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="pr/903">
                pr/903
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/rkung-ibm-patch-1/services/mobileaccess/google-auth-overview.md"
               data-name="rkung-ibm-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="rkung-ibm-patch-1">
                rkung-ibm-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/rkung-ibm-patch-2/services/mobileaccess/google-auth-overview.md"
               data-name="rkung-ibm-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="rkung-ibm-patch-2">
                rkung-ibm-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/rkung-ibm-patch-3/services/mobileaccess/google-auth-overview.md"
               data-name="rkung-ibm-patch-3"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="rkung-ibm-patch-3">
                rkung-ibm-patch-3
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/rkung-ibm-patch-4/services/mobileaccess/google-auth-overview.md"
               data-name="rkung-ibm-patch-4"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="rkung-ibm-patch-4">
                rkung-ibm-patch-4
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/rkung-ibm-patch-5/services/mobileaccess/google-auth-overview.md"
               data-name="rkung-ibm-patch-5"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="rkung-ibm-patch-5">
                rkung-ibm-patch-5
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/rti-accessibility/services/mobileaccess/google-auth-overview.md"
               data-name="rti-accessibility"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="rti-accessibility">
                rti-accessibility
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/rti-migration/services/mobileaccess/google-auth-overview.md"
               data-name="rti-migration"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="rti-migration">
                rti-migration
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sefuhrer-fix-to-h1-and-date/services/mobileaccess/google-auth-overview.md"
               data-name="sefuhrer-fix-to-h1-and-date"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="sefuhrer-fix-to-h1-and-date">
                sefuhrer-fix-to-h1-and-date
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sefuhrer-fixed-markdown-link-nested-in-HTML/services/mobileaccess/google-auth-overview.md"
               data-name="sefuhrer-fixed-markdown-link-nested-in-HTML"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="sefuhrer-fixed-markdown-link-nested-in-HTML">
                sefuhrer-fixed-markdown-link-nested-in-HTML
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sefuhrer-fixes-to-h1/services/mobileaccess/google-auth-overview.md"
               data-name="sefuhrer-fixes-to-h1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="sefuhrer-fixes-to-h1">
                sefuhrer-fixes-to-h1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sefuhrer-patch-1/services/mobileaccess/google-auth-overview.md"
               data-name="sefuhrer-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="sefuhrer-patch-1">
                sefuhrer-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sjfink-patch-1/services/mobileaccess/google-auth-overview.md"
               data-name="sjfink-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="sjfink-patch-1">
                sjfink-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sjfink-patch-2/services/mobileaccess/google-auth-overview.md"
               data-name="sjfink-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="sjfink-patch-2">
                sjfink-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sktay-patch-1/services/mobileaccess/google-auth-overview.md"
               data-name="sktay-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="sktay-patch-1">
                sktay-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sktay-patch-2/services/mobileaccess/google-auth-overview.md"
               data-name="sktay-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="sktay-patch-2">
                sktay-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sktay/services/mobileaccess/google-auth-overview.md"
               data-name="sktay"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="sktay">
                sktay
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/smguilia-patch-1/services/mobileaccess/google-auth-overview.md"
               data-name="smguilia-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="smguilia-patch-1">
                smguilia-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/smguilia-patch-2/services/mobileaccess/google-auth-overview.md"
               data-name="smguilia-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="smguilia-patch-2">
                smguilia-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/vagrant/services/mobileaccess/google-auth-overview.md"
               data-name="vagrant"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="vagrant">
                vagrant
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/whisk_eventbased/services/mobileaccess/google-auth-overview.md"
               data-name="whisk_eventbased"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="whisk_eventbased">
                whisk_eventbased
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/wilburnvanessa-patch-1/services/mobileaccess/google-auth-overview.md"
               data-name="wilburnvanessa-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="wilburnvanessa-patch-1">
                wilburnvanessa-patch-1
              </span>
            </a>
        </div>

          <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/IBM-Bluemix/docs-staging/branches" class="js-create-branch select-menu-item select-menu-new-item-form js-navigation-item js-new-item-form" data-form-nonce="9d725a0f2ec9cef3ada60ee7c58b904f69bd9c48" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="T3FV9a9313MPmLwYHE+c2vO1Rj+86pKbFEBDh7NpzeaKTGj0/uc+SFjAZUzrcEykLmawrQTgxSsjp2siOeHmzQ==" /></div>
          <svg aria-hidden="true" class="octicon octicon-git-branch select-menu-item-icon" height="16" version="1.1" viewBox="0 0 10 16" width="10"><path d="M10 5c0-1.11-.89-2-2-2a1.993 1.993 0 0 0-1 3.72v.3c-.02.52-.23.98-.63 1.38-.4.4-.86.61-1.38.63-.83.02-1.48.16-2 .45V4.72a1.993 1.993 0 0 0-1-3.72C.88 1 0 1.89 0 3a2 2 0 0 0 1 1.72v6.56c-.59.35-1 .99-1 1.72 0 1.11.89 2 2 2 1.11 0 2-.89 2-2 0-.53-.2-1-.53-1.36.09-.06.48-.41.59-.47.25-.11.56-.17.94-.17 1.05-.05 1.95-.45 2.75-1.25S8.95 7.77 9 6.73h-.02C9.59 6.37 10 5.73 10 5zM2 1.8c.66 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2C1.35 4.2.8 3.65.8 3c0-.65.55-1.2 1.2-1.2zm0 12.41c-.66 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2zm6-8c-.66 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2z"></path></svg>
            <div class="select-menu-item-text">
              <span class="select-menu-item-heading">Create branch: <span class="js-new-item-name"></span></span>
              <span class="description">from ‘master’</span>
            </div>
            <input type="hidden" name="name" id="name" class="js-new-item-value">
            <input type="hidden" name="branch" id="branch" value="master">
            <input type="hidden" name="path" id="path" value="services/mobileaccess/google-auth-overview.md">
</form>
      </div>

      <div class="select-menu-list select-menu-tab-bucket js-select-menu-tab-bucket" data-tab-filter="tags">
        <div data-filterable-for="context-commitish-filter-field" data-filterable-type="substring">


        </div>

        <div class="select-menu-no-results">Nothing to show</div>
      </div>

    </div>
  </div>
</div>

  <div class="btn-group right">
    <a href="/IBM-Bluemix/docs-staging/find/master"
          class="js-pjax-capture-input btn btn-sm"
          data-pjax
          data-hotkey="t">
      Find file
    </a>
    <button aria-label="Copy file path to clipboard" class="js-zeroclipboard btn btn-sm zeroclipboard-button tooltipped tooltipped-s" data-copied-hint="Copied!" type="button">Copy path</button>
  </div>
  <div class="breadcrumb js-zeroclipboard-target">
    <span class="repo-root js-repo-root"><span class="js-path-segment"><a href="/IBM-Bluemix/docs-staging"><span>docs-staging</span></a></span></span><span class="separator">/</span><span class="js-path-segment"><a href="/IBM-Bluemix/docs-staging/tree/master/services"><span>services</span></a></span><span class="separator">/</span><span class="js-path-segment"><a href="/IBM-Bluemix/docs-staging/tree/master/services/mobileaccess"><span>mobileaccess</span></a></span><span class="separator">/</span><strong class="final-path">google-auth-overview.md</strong>
  </div>
</div>

<include-fragment class="commit-tease" src="/IBM-Bluemix/docs-staging/contributors/master/services/mobileaccess/google-auth-overview.md">
  <div>
    Fetching contributors&hellip;
  </div>

  <div class="commit-tease-contributors">
    <img alt="" class="loader-loading left" height="16" src="https://assets-cdn.github.com/images/spinners/octocat-spinner-32-EAF2F5.gif" width="16" />
    <span class="loader-error">Cannot retrieve contributors at this time</span>
  </div>
</include-fragment>
<div class="file">
  <div class="file-header">
  <div class="file-actions">

    <div class="btn-group">
      <a href="/IBM-Bluemix/docs-staging/raw/master/services/mobileaccess/google-auth-overview.md" class="btn btn-sm " id="raw-url">Raw</a>
        <a href="/IBM-Bluemix/docs-staging/blame/master/services/mobileaccess/google-auth-overview.md" class="btn btn-sm js-update-url-with-hash">Blame</a>
      <a href="/IBM-Bluemix/docs-staging/commits/master/services/mobileaccess/google-auth-overview.md" class="btn btn-sm " rel="nofollow">History</a>
    </div>

        <a class="btn-octicon tooltipped tooltipped-nw"
           href="github-windows://openRepo/https://github.com/IBM-Bluemix/docs-staging?branch=master&amp;filepath=services%2Fmobileaccess%2Fgoogle-auth-overview.md"
           aria-label="Open this file in GitHub Desktop"
           data-ga-click="Repository, open with desktop, type:windows">
            <svg aria-hidden="true" class="octicon octicon-device-desktop" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M15 2H1c-.55 0-1 .45-1 1v9c0 .55.45 1 1 1h5.34c-.25.61-.86 1.39-2.34 2h8c-1.48-.61-2.09-1.39-2.34-2H15c.55 0 1-.45 1-1V3c0-.55-.45-1-1-1zm0 9H1V3h14v8z"></path></svg>
        </a>

        <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/IBM-Bluemix/docs-staging/edit/master/services/mobileaccess/google-auth-overview.md" class="inline-form js-update-url-with-hash" data-form-nonce="9d725a0f2ec9cef3ada60ee7c58b904f69bd9c48" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="DDPEmlvf5VaGdjrwLllJkx29rMoDAD7i4qsdEFJrQ/ZgEd8KkyfPggqNtqPgm94+A+wRW85shGc6gcHip6qYCQ==" /></div>
          <button class="btn-octicon tooltipped tooltipped-nw" type="submit"
            aria-label="Edit this file" data-hotkey="e" data-disable-with>
            <svg aria-hidden="true" class="octicon octicon-pencil" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path d="M0 12v3h3l8-8-3-3-8 8zm3 2H1v-2h1v1h1v1zm10.3-9.3L12 6 9 3l1.3-1.3a.996.996 0 0 1 1.41 0l1.59 1.59c.39.39.39 1.02 0 1.41z"></path></svg>
          </button>
</form>        <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/IBM-Bluemix/docs-staging/delete/master/services/mobileaccess/google-auth-overview.md" class="inline-form" data-form-nonce="9d725a0f2ec9cef3ada60ee7c58b904f69bd9c48" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="4lANDePF1bjodtntIBO/cFcfV5yKJFhe2GHvu6Gq+jdnWt9zpElZIBkqAxkawmI6SE3IueZeO8ZgS10g9vU/JA==" /></div>
          <button class="btn-octicon btn-octicon-danger tooltipped tooltipped-nw" type="submit"
            aria-label="Delete this file" data-disable-with>
            <svg aria-hidden="true" class="octicon octicon-trashcan" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M11 2H9c0-.55-.45-1-1-1H5c-.55 0-1 .45-1 1H2c-.55 0-1 .45-1 1v1c0 .55.45 1 1 1v9c0 .55.45 1 1 1h7c.55 0 1-.45 1-1V5c.55 0 1-.45 1-1V3c0-.55-.45-1-1-1zm-1 12H3V5h1v8h1V5h1v8h1V5h1v8h1V5h1v9zm1-10H2V3h9v1z"></path></svg>
          </button>
</form>  </div>

  <div class="file-info">
      61 lines (41 sloc)
      <span class="file-info-divider"></span>
    3.71 KB
  </div>
</div>

  
  <div id="readme" class="readme blob instapaper_body">
    <article class="markdown-body entry-content" itemprop="text"><table data-table-type="yaml-metadata">
  <thead>
  <tr>
  <th>copyright</th>
  </tr>
  </thead>
  <tbody>
  <tr>
  <td><div><table>
  <thead>
  <tr>
  <th>years</th>
  </tr>
  </thead>
  <tbody>
  <tr>
  <td><div>2015, 2016</div></td>
  </tr>
  </tbody>
</table></div></td>
  </tr>
  </tbody>
</table>

<p>{:screen:  .screen}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}</p>

<h1><a id="user-content-authenticating-users-with-google-credentials" class="anchor" href="#authenticating-users-with-google-credentials" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Authenticating users with Google credentials</h1>

<p>{: #google-auth}</p>

<p><em>Last updated: 20 July 2016</em></p>

<p>You can configure the {{site.data.keyword.amashort}} service to protect resources, using Google as an identity provider. Your mobile or web application users can then use their Google credentials for authentication.
{:shortdesc}</p>

<p><strong>Important:</strong> You do not need to separately install the Google SDK. The Google SDK is installed automatically by dependency managers when you configure the {{site.data.keyword.amashort}} client SDK.</p>

<h2><a id="user-content-sitedatakeywordamashort--request-flow" class="anchor" href="#sitedatakeywordamashort--request-flow" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>{{site.data.keyword.amashort}}  request flow</h2>

<p>{: #google-auth-overview}</p>

<h3><a id="user-content-client-request-flow" class="anchor" href="#client-request-flow" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Client request flow</h3>

<p>See the following simplified diagram to understand how {{site.data.keyword.amashort}} integrates with Google for authentication.</p>

<p><a href="/IBM-Bluemix/docs-staging/blob/master/services/mobileaccess/images/mca-sequence-google.jpg" target="_blank"><img src="/IBM-Bluemix/docs-staging/raw/master/services/mobileaccess/images/mca-sequence-google.jpg" alt="image" style="max-width:100%;"></a></p>

<ol>
<li>Use the {{site.data.keyword.amashort}} SDK to make a request to your back-end resources that are protected  with the {{site.data.keyword.amashort}} server SDK.</li>
<li>The {{site.data.keyword.amashort}} server SDK detects the unauthorized request and returns an HTTP 401 code and authorization scope.</li>
<li>The {{site.data.keyword.amashort}} client SDK automatically detects the HTTP 401 code and starts the authentication process.</li>
<li>The {{site.data.keyword.amashort}} client SDK  contacts the {{site.data.keyword.amashort}} service and requests an authorization header.</li>
<li>The {{site.data.keyword.amashort}} service asks the client to authenticate with Google first by supplying an authentication challenge.</li>
<li>The {{site.data.keyword.amashort}} client SDK uses the Google SDK to start the authentication process. After successful authentication, the Google SDK returns a Google access token.</li>
<li>The Google access token is considered an authentication challenge answer. The token is sent to the {{site.data.keyword.amashort}} service.</li>
<li>The service validates the authentication challenge answer with Google servers.</li>
<li>If validation is successful, the {{site.data.keyword.amashort}} service generates an authorization header and returns it to the {{site.data.keyword.amashort}} client SDK. The authorization header contains two tokens: an access token that contains access permissions information, and ID token that contains information about the current user, device, and application.</li>
<li>From this point on, all requests that are made through the {{site.data.keyword.amashort}} client SDK  have a newly obtained authorization header.</li>
<li>The {{site.data.keyword.amashort}} client SDK automatically resends the original request that triggered the authorization flow.</li>
<li>The {{site.data.keyword.amashort}} server SDK extracts the authorization header from the request, validates it with the {{site.data.keyword.amashort}} service, and grants access to a back-end resource.</li>
</ol>

<h3><a id="user-content-sitedatakeywordamashort-web-application-request-flow" class="anchor" href="#sitedatakeywordamashort-web-application-request-flow" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>{{site.data.keyword.amashort}} web application request flow</h3>

<p>{: #mca-google-web-sequence}
The {{site.data.keyword.amashort}} web application request flow is similar to the mobile client flow. However, {{site.data.keyword.amashort}} protects the web application, rather than a {{site.data.keyword.Bluemix_notm}} back-end resource.</p>

<ul>
<li>The initial request is sent by the web application (from a log-in form, for example).</li>
<li>The final redirect is to the protected area of the web application itself, rather than back-end protected resource. </li>
</ul>

<h2><a id="user-content-next-steps" class="anchor" href="#next-steps" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Next steps</h2>

<p>{: #google-auth-nextsteps}</p>

<ul>
<li><a href="/IBM-Bluemix/docs-staging/blob/master/services/mobileaccess/google-auth-android.html">Enabling Google authentication for Android apps</a></li>
<li><a href="/IBM-Bluemix/docs-staging/blob/master/services/mobileaccess/google-auth-ios-swift-sdk.html">Enabling Google authentication for iOS apps (Swift SDK)</a></li>
<li><a href="/IBM-Bluemix/docs-staging/blob/master/services/mobileaccess/google-auth-ios.html">Enabling Google authentication for iOS apps (Objective-C SDK)</a></li>
<li><a href="/IBM-Bluemix/docs-staging/blob/master/services/mobileaccess/google-auth-cordova.html">Enabling Google authentication for Cordova apps</a></li>
</ul>
</article>
  </div>

</div>

<button type="button" data-facebox="#jump-to-line" data-facebox-class="linejump" data-hotkey="l" class="hidden">Jump to Line</button>
<div id="jump-to-line" style="display:none">
  <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="" class="js-jump-to-line-form" method="get"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /></div>
    <input class="form-control linejump-input js-jump-to-line-field" type="text" placeholder="Jump to line&hellip;" aria-label="Jump to line" autofocus>
    <button type="submit" class="btn">Go</button>
</form></div>

  </div>
  <div class="modal-backdrop js-touch-events"></div>
</div>


    </div>
  </div>

    </div>

        <div class="container site-footer-container">
  <div class="site-footer" role="contentinfo">
    <ul class="site-footer-links right">
        <li><a href="https://github.com/contact" data-ga-click="Footer, go to contact, text:contact">Contact GitHub</a></li>
      <li><a href="https://developer.github.com" data-ga-click="Footer, go to api, text:api">API</a></li>
      <li><a href="https://training.github.com" data-ga-click="Footer, go to training, text:training">Training</a></li>
      <li><a href="https://shop.github.com" data-ga-click="Footer, go to shop, text:shop">Shop</a></li>
        <li><a href="https://github.com/blog" data-ga-click="Footer, go to blog, text:blog">Blog</a></li>
        <li><a href="https://github.com/about" data-ga-click="Footer, go to about, text:about">About</a></li>

    </ul>

    <a href="https://github.com" aria-label="Homepage" class="site-footer-mark" title="GitHub">
      <svg aria-hidden="true" class="octicon octicon-mark-github" height="24" version="1.1" viewBox="0 0 16 16" width="24"><path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0 0 16 8c0-4.42-3.58-8-8-8z"></path></svg>
</a>
    <ul class="site-footer-links">
      <li>&copy; 2016 <span title="0.10646s from github-fe133-cp1-prd.iad.github.net">GitHub</span>, Inc.</li>
        <li><a href="https://github.com/site/terms" data-ga-click="Footer, go to terms, text:terms">Terms</a></li>
        <li><a href="https://github.com/site/privacy" data-ga-click="Footer, go to privacy, text:privacy">Privacy</a></li>
        <li><a href="https://github.com/security" data-ga-click="Footer, go to security, text:security">Security</a></li>
        <li><a href="https://status.github.com/" data-ga-click="Footer, go to status, text:status">Status</a></li>
        <li><a href="https://help.github.com" data-ga-click="Footer, go to help, text:help">Help</a></li>
    </ul>
  </div>
</div>



    

    <div id="ajax-error-message" class="ajax-error-message flash flash-error">
      <svg aria-hidden="true" class="octicon octicon-alert" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M8.865 1.52c-.18-.31-.51-.5-.87-.5s-.69.19-.87.5L.275 13.5c-.18.31-.18.69 0 1 .19.31.52.5.87.5h13.7c.36 0 .69-.19.86-.5.17-.31.18-.69.01-1L8.865 1.52zM8.995 13h-2v-2h2v2zm0-3h-2V6h2v4z"></path></svg>
      <button type="button" class="flash-close js-flash-close js-ajax-error-dismiss" aria-label="Dismiss error">
        <svg aria-hidden="true" class="octicon octicon-x" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M7.48 8l3.75 3.75-1.48 1.48L6 9.48l-3.75 3.75-1.48-1.48L4.52 8 .77 4.25l1.48-1.48L6 6.52l3.75-3.75 1.48 1.48z"></path></svg>
      </button>
      Something went wrong with that request. Please try again.
    </div>


      
      <script crossorigin="anonymous" integrity="sha256-QEzdGt0fcQ2wFqAuXjH/+KkInRT/DCJ9+GK3gIhtt9U=" src="https://assets-cdn.github.com/assets/frameworks-404cdd1add1f710db016a02e5e31fff8a9089d14ff0c227df862b780886db7d5.js"></script>
      <script async="async" crossorigin="anonymous" integrity="sha256-vabI89d3JD+RkvdyXWgGc6oTOU6u7lCB5T8A5C6VACg=" src="https://assets-cdn.github.com/assets/github-bda6c8f3d777243f9192f7725d680673aa13394eaeee5081e53f00e42e950028.js"></script>
      
      
      
      
      
      
    <div class="js-stale-session-flash stale-session-flash flash flash-warn flash-banner hidden">
      <svg aria-hidden="true" class="octicon octicon-alert" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M8.865 1.52c-.18-.31-.51-.5-.87-.5s-.69.19-.87.5L.275 13.5c-.18.31-.18.69 0 1 .19.31.52.5.87.5h13.7c.36 0 .69-.19.86-.5.17-.31.18-.69.01-1L8.865 1.52zM8.995 13h-2v-2h2v2zm0-3h-2V6h2v4z"></path></svg>
      <span class="signed-in-tab-flash">You signed in with another tab or window. <a href="">Reload</a> to refresh your session.</span>
      <span class="signed-out-tab-flash">You signed out in another tab or window. <a href="">Reload</a> to refresh your session.</span>
    </div>
    <div class="facebox" id="facebox" style="display:none;">
  <div class="facebox-popup">
    <div class="facebox-content" role="dialog" aria-labelledby="facebox-header" aria-describedby="facebox-description">
    </div>
    <button type="button" class="facebox-close js-facebox-close" aria-label="Close modal">
      <svg aria-hidden="true" class="octicon octicon-x" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M7.48 8l3.75 3.75-1.48 1.48L6 9.48l-3.75 3.75-1.48-1.48L4.52 8 .77 4.25l1.48-1.48L6 6.52l3.75-3.75 1.48 1.48z"></path></svg>
    </button>
  </div>
</div>

  </body>
</html>

