



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
    
    <title>docs-staging/google-auth-ios-swift-sdk.md at master · IBM-Bluemix/docs-staging</title>
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
    <link rel="web-socket" href="wss://live.github.com/_sockets/MTY4NjMwNzg6MDZhOWJkMDQwOTRiOTRhNTkyZTllYzVlNzc1NDdhZjM6YzAwNjZmZjFiNGYzODA1MzAyMmRlMDlmYWE1MjhjNjRiZDE4NzgxNGMzZDdkZDRkMWQwZTliODhkOWUwOTEyOQ==--c009d9bf4928969595176a4f98e80b65f8f72311">
    <meta name="pjax-timeout" content="1000">
    <link rel="sudo-modal" href="/sessions/sudo_modal">

    <meta name="msapplication-TileImage" content="/windows-tile.png">
    <meta name="msapplication-TileColor" content="#ffffff">
    <meta name="selected-link" value="repo_source" data-pjax-transient>

    <meta name="google-site-verification" content="KT5gs8h0wvaagLKAVWq8bbeNwnZZK1r1XQysX3xurLU">
<meta name="google-site-verification" content="ZzhVyEFwb7w3e0-uOTltm8Jsck2F5StVihD0exw2fsA">
    <meta name="google-analytics" content="UA-3769691-2">

<meta content="collector.githubapp.com" name="octolytics-host" /><meta content="github" name="octolytics-app-id" /><meta content="C36E28F6:2BC4:6CC58B1:5790BE2B" name="octolytics-dimension-request_id" /><meta content="16863078" name="octolytics-actor-id" /><meta content="jergirl" name="octolytics-actor-login" /><meta content="d11eb53b80aa964bb40a401c764876267e504da721f7d9079e2540cc373ceb97" name="octolytics-actor-hash" />
<meta content="/&lt;user-name&gt;/&lt;repo-name&gt;/blob/show" data-pjax-transient="true" name="analytics-location" />



  <meta class="js-ga-set" name="dimension1" content="Logged In">



        <meta name="hostname" content="github.com">
    <meta name="user-login" content="jergirl">

        <meta name="expected-hostname" content="github.com">
      <meta name="js-proxy-site-detection-payload" content="ZTY5MDkyZDIwZWFhYTc2MGQ5M2QxYjY5ODg2MzU4M2VmMzc1YWU5OGE0ZmFjYWRlZmY1NDU0YWQ3YzM2Y2U4OXx7InJlbW90ZV9hZGRyZXNzIjoiMTk1LjExMC40MC4yNDYiLCJyZXF1ZXN0X2lkIjoiQzM2RTI4RjY6MkJDNDo2Q0M1OEIxOjU3OTBCRTJCIiwidGltZXN0YW1wIjoxNDY5MTAzNjU5fQ==">


      <link rel="mask-icon" href="https://assets-cdn.github.com/pinned-octocat.svg" color="#4078c0">
      <link rel="icon" type="image/x-icon" href="https://assets-cdn.github.com/favicon.ico">

    <meta name="html-safe-nonce" content="63c716447c96747282ba696a86a155a2d7a53e30">
    <meta content="9d725a0f2ec9cef3ada60ee7c58b904f69bd9c48" name="form-nonce" />

    <meta http-equiv="x-pjax-version" content="c85c9b6f8432cc7b07e5ce5161e4d4fc">
    

      
  <meta name="description" content="docs-staging - IBM Bluemix documentation on the staging app.">
  <meta name="go-import" content="github.com/IBM-Bluemix/docs-staging git https://github.com/IBM-Bluemix/docs-staging.git">

  <meta content="7284885" name="octolytics-dimension-user_id" /><meta content="IBM-Bluemix" name="octolytics-dimension-user_login" /><meta content="39894162" name="octolytics-dimension-repository_id" /><meta content="IBM-Bluemix/docs-staging" name="octolytics-dimension-repository_nwo" /><meta content="false" name="octolytics-dimension-repository_public" /><meta content="false" name="octolytics-dimension-repository_is_fork" /><meta content="39894162" name="octolytics-dimension-repository_network_root_id" /><meta content="IBM-Bluemix/docs-staging" name="octolytics-dimension-repository_network_root_nwo" />
  <link href="https://github.com/IBM-Bluemix/docs-staging/commits/master.atom?token=AQFPZlClXdrR0sNpmtOp39O1g72BvPP7ks61nK07wA%3D%3D" rel="alternate" title="Recent Commits to docs-staging:master" type="application/atom+xml">


      <link rel="canonical" href="https://github.com/IBM-Bluemix/docs-staging/blob/master/services/mobileaccess/google-auth-ios-swift-sdk.md" data-pjax-transient>
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

        <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/logout" class="logout-form" data-form-nonce="9d725a0f2ec9cef3ada60ee7c58b904f69bd9c48" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="D9tUs41WumBPPt4VE91++QAl9ACamgDj40kdR8INQU2HTtU2Qu5yE0AHL3N8krQP81G0QueNXlgSLV+Y4w82ZA==" /></div>
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
        <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/notifications/subscribe" class="js-social-container" data-autosubmit="true" data-form-nonce="9d725a0f2ec9cef3ada60ee7c58b904f69bd9c48" data-remote="true" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="JCZhNkYZFk3RQ/JYGl584DWdV7R7dd4LiDGQVqhCxbkhz+HblSQm8Y5L/+J1pjFAGFGK8rXWhMP54BX9CzqSpw==" /></div>      <input class="form-control" id="repository_id" name="repository_id" type="hidden" value="39894162" />

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

    <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/IBM-Bluemix/docs-staging/unstar" class="starred" data-form-nonce="9d725a0f2ec9cef3ada60ee7c58b904f69bd9c48" data-remote="true" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="ajRjJ3GF73wiFvgmLQECc13253vP/bVxQ1kINOqWfWsTLmFJK0GWsXfLk5pnPXWz9S7TiUOX6X8N7VELKKnnRw==" /></div>
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
    <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/IBM-Bluemix/docs-staging/star" class="unstarred" data-form-nonce="9d725a0f2ec9cef3ada60ee7c58b904f69bd9c48" data-remote="true" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="9hY89cnm3rhB4qACu1A5Cv1RZ9N3UOUop+aV1q2xVPWqunVM07nhZ6gwuAn18ieyO8B5bFS7XTtcDzGKiM3mpA==" /></div>
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

    

<a href="/IBM-Bluemix/docs-staging/blob/a28236bc9b6b9d372219f671f7db045e4b35d8ae/services/mobileaccess/google-auth-ios-swift-sdk.md" class="hidden js-permalink-shortcut" data-hotkey="y">Permalink</a>

<!-- blob contrib key: blob_contributors:v21:a18be9ffc40bb33269dd74ede11eaa81 -->

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
               href="/IBM-Bluemix/docs-staging/blob/148440-update-docs-to-reflect-removal-of-V1-APIs-/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="148440-update-docs-to-reflect-removal-of-V1-APIs-"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="148440-update-docs-to-reflect-removal-of-V1-APIs-">
                148440-update-docs-to-reflect-removal-of-V1-APIs-
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/201357-cfapps-runtimes-viewdocs/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="201357-cfapps-runtimes-viewdocs"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="201357-cfapps-runtimes-viewdocs">
                201357-cfapps-runtimes-viewdocs
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/204629-starters-to-runtimes/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="204629-starters-to-runtimes"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="204629-starters-to-runtimes">
                204629-starters-to-runtimes
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/212031-cfapps-runtimes/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="212031-cfapps-runtimes"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="212031-cfapps-runtimes">
                212031-cfapps-runtimes
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/212368-addressedViolationInCodeBlockForLiberty/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="212368-addressedViolationInCodeBlockForLiberty"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="212368-addressedViolationInCodeBlockForLiberty">
                212368-addressedViolationInCodeBlockForLiberty
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/213742-removeNewlines/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="213742-removeNewlines"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="213742-removeNewlines">
                213742-removeNewlines
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/218761-link-proxy/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="218761-link-proxy"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="218761-link-proxy">
                218761-link-proxy
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/218862-RemoveBulletForPsirt/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="218862-RemoveBulletForPsirt"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="218862-RemoveBulletForPsirt">
                218862-RemoveBulletForPsirt
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/218862-latestUpdate-v9/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="218862-latestUpdate-v9"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="218862-latestUpdate-v9">
                218862-latestUpdate-v9
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Caroline-July-work/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="Caroline-July-work"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="Caroline-July-work">
                Caroline-July-work
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Creation-of-IoT-for-Automotive-Getting-Started-docs/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="Creation-of-IoT-for-Automotive-Getting-Started-docs"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="Creation-of-IoT-for-Automotive-Getting-Started-docs">
                Creation-of-IoT-for-Automotive-Getting-Started-docs
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Crystal4545-patch-1/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="Crystal4545-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="Crystal4545-patch-1">
                Crystal4545-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Crystal4545-patch-2/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="Crystal4545-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="Crystal4545-patch-2">
                Crystal4545-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Crystal4545-patch-3/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="Crystal4545-patch-3"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="Crystal4545-patch-3">
                Crystal4545-patch-3
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Crystal4545/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="Crystal4545"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="Crystal4545">
                Crystal4545
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/ID-edits-to-Driver-Behaviour-overview-docs/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="ID-edits-to-Driver-Behaviour-overview-docs"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="ID-edits-to-Driver-Behaviour-overview-docs">
                ID-edits-to-Driver-Behaviour-overview-docs
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/ID-edits-to-Map-insights-docs/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="ID-edits-to-Map-insights-docs"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="ID-edits-to-Map-insights-docs">
                ID-edits-to-Map-insights-docs
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/MPurcell-ID-editing-and-technical-updates-to-Blockchain-contracts-docs/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="MPurcell-ID-editing-and-technical-updates-to-Blockchain-contracts-docs"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="MPurcell-ID-editing-and-technical-updates-to-Blockchain-contracts-docs">
                MPurcell-ID-editing-and-technical-updates-to-Blockchain-contracts-docs
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Sec-bluemix-ed/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="Sec-bluemix-ed"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="Sec-bluemix-ed">
                Sec-bluemix-ed
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Updates-and-edits-to-new-Driver-Behavior-admin-feature/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="Updates-and-edits-to-new-Driver-Behavior-admin-feature"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="Updates-and-edits-to-new-Driver-Behavior-admin-feature">
                Updates-and-edits-to-new-Driver-Behavior-admin-feature
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/automotive-ID-review/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="automotive-ID-review"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="automotive-ID-review">
                automotive-ID-review
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/benbakowski-patch-2/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="benbakowski-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="benbakowski-patch-2">
                benbakowski-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/bhpratt-patch-1/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="bhpratt-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="bhpratt-patch-1">
                bhpratt-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/bhpratt-patch-2/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="bhpratt-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="bhpratt-patch-2">
                bhpratt-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/bwentwor-patch-1/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="bwentwor-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="bwentwor-patch-1">
                bwentwor-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/danawilson-patch-1/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="danawilson-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="danawilson-patch-1">
                danawilson-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/fix_limits_table/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="fix_limits_table"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="fix_limits_table">
                fix_limits_table
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/fixMyIssue/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="fixMyIssue"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="fixMyIssue">
                fixMyIssue
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/gcatasta-patternengine/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="gcatasta-patternengine"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="gcatasta-patternengine">
                gcatasta-patternengine
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/gshgui-patch-1/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="gshgui-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="gshgui-patch-1">
                gshgui-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/iot-edge-analytics-addition/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="iot-edge-analytics-addition"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="iot-edge-analytics-addition">
                iot-edge-analytics-addition
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/iot-initial/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="iot-initial"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="iot-initial">
                iot-initial
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/iot-nav-changes/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="iot-nav-changes"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="iot-nav-changes">
                iot-nav-changes
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/iot-platform-blockchain-merger/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="iot-platform-blockchain-merger"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="iot-platform-blockchain-merger">
                iot-platform-blockchain-merger
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/iot-platform-security-iso/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="iot-platform-security-iso"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="iot-platform-security-iso">
                iot-platform-security-iso
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/it8-changes/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="it8-changes"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="it8-changes">
                it8-changes
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/it9-changes/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="it9-changes"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="it9-changes">
                it9-changes
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jbetht-patch-1/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="jbetht-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="jbetht-patch-1">
                jbetht-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jbetht-patch-2-1/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="jbetht-patch-2-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="jbetht-patch-2-1">
                jbetht-patch-2-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jbetht-patch-2/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="jbetht-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="jbetht-patch-2">
                jbetht-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jbetht-patch-3/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="jbetht-patch-3"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="jbetht-patch-3">
                jbetht-patch-3
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jbetht-patch-8/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="jbetht-patch-8"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="jbetht-patch-8">
                jbetht-patch-8
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jeffchi-patch-1/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="jeffchi-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="jeffchi-patch-1">
                jeffchi-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jgchan-merge-staging-to-production/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="jgchan-merge-staging-to-production"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="jgchan-merge-staging-to-production">
                jgchan-merge-staging-to-production
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jsg-branch/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="jsg-branch"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="jsg-branch">
                jsg-branch
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jsg-can-patch-1/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="jsg-can-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="jsg-can-patch-1">
                jsg-can-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/kKronstainBrown-patch-1/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="kKronstainBrown-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="kKronstainBrown-patch-1">
                kKronstainBrown-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/kKronstainBrown-patch-2/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="kKronstainBrown-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="kKronstainBrown-patch-2">
                kKronstainBrown-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/knlyons/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="knlyons"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="knlyons">
                knlyons
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/last_minute_rules_action_changes/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="last_minute_rules_action_changes"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="last_minute_rules_action_changes">
                last_minute_rules_action_changes
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/lopezdsr-patch-1/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="lopezdsr-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="lopezdsr-patch-1">
                lopezdsr-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/lopezdsr-patch-3/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="lopezdsr-patch-3"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="lopezdsr-patch-3">
                lopezdsr-patch-3
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open selected"
               href="/IBM-Bluemix/docs-staging/blob/master/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="master"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="master">
                master
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/mdb-DRA-jenkins/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="mdb-DRA-jenkins"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="mdb-DRA-jenkins">
                mdb-DRA-jenkins
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/mekaufman-patch-1/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="mekaufman-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="mekaufman-patch-1">
                mekaufman-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/mpurcell-edits-to-improve-python-docs/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="mpurcell-edits-to-improve-python-docs"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="mpurcell-edits-to-improve-python-docs">
                mpurcell-edits-to-improve-python-docs
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/mpurcell-new-client-connection-topic/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="mpurcell-new-client-connection-topic"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="mpurcell-new-client-connection-topic">
                mpurcell-new-client-connection-topic
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/mpurcell-technical-dev-doc-edits-for-GA-release/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="mpurcell-technical-dev-doc-edits-for-GA-release"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="mpurcell-technical-dev-doc-edits-for-GA-release">
                mpurcell-technical-dev-doc-edits-for-GA-release
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/mpurcell-updates-to-automotive-services-for-release-refreshes-22nd-july/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="mpurcell-updates-to-automotive-services-for-release-refreshes-22nd-july"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="mpurcell-updates-to-automotive-services-for-release-refreshes-22nd-july">
                mpurcell-updates-to-automotive-services-for-release-refreshes-22nd-july
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/offlinemode/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="offlinemode"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="offlinemode">
                offlinemode
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/pr/481/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="pr/481"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="pr/481">
                pr/481
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/pr/661/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="pr/661"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="pr/661">
                pr/661
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/pr/903/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="pr/903"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="pr/903">
                pr/903
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/rkung-ibm-patch-1/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="rkung-ibm-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="rkung-ibm-patch-1">
                rkung-ibm-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/rkung-ibm-patch-2/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="rkung-ibm-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="rkung-ibm-patch-2">
                rkung-ibm-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/rkung-ibm-patch-3/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="rkung-ibm-patch-3"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="rkung-ibm-patch-3">
                rkung-ibm-patch-3
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/rkung-ibm-patch-4/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="rkung-ibm-patch-4"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="rkung-ibm-patch-4">
                rkung-ibm-patch-4
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/rkung-ibm-patch-5/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="rkung-ibm-patch-5"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="rkung-ibm-patch-5">
                rkung-ibm-patch-5
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/rti-accessibility/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="rti-accessibility"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="rti-accessibility">
                rti-accessibility
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/rti-migration/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="rti-migration"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="rti-migration">
                rti-migration
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sefuhrer-fix-to-h1-and-date/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="sefuhrer-fix-to-h1-and-date"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="sefuhrer-fix-to-h1-and-date">
                sefuhrer-fix-to-h1-and-date
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sefuhrer-fixed-markdown-link-nested-in-HTML/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="sefuhrer-fixed-markdown-link-nested-in-HTML"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="sefuhrer-fixed-markdown-link-nested-in-HTML">
                sefuhrer-fixed-markdown-link-nested-in-HTML
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sefuhrer-fixes-to-h1/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="sefuhrer-fixes-to-h1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="sefuhrer-fixes-to-h1">
                sefuhrer-fixes-to-h1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sefuhrer-patch-1/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="sefuhrer-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="sefuhrer-patch-1">
                sefuhrer-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sjfink-patch-1/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="sjfink-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="sjfink-patch-1">
                sjfink-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sjfink-patch-2/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="sjfink-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="sjfink-patch-2">
                sjfink-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sktay-patch-1/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="sktay-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="sktay-patch-1">
                sktay-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sktay-patch-2/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="sktay-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="sktay-patch-2">
                sktay-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sktay/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="sktay"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="sktay">
                sktay
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/smguilia-patch-1/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="smguilia-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="smguilia-patch-1">
                smguilia-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/smguilia-patch-2/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="smguilia-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="smguilia-patch-2">
                smguilia-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/vagrant/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="vagrant"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="vagrant">
                vagrant
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/whisk_eventbased/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="whisk_eventbased"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="whisk_eventbased">
                whisk_eventbased
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/wilburnvanessa-patch-1/services/mobileaccess/google-auth-ios-swift-sdk.md"
               data-name="wilburnvanessa-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"></path></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text" title="wilburnvanessa-patch-1">
                wilburnvanessa-patch-1
              </span>
            </a>
        </div>

          <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/IBM-Bluemix/docs-staging/branches" class="js-create-branch select-menu-item select-menu-new-item-form js-navigation-item js-new-item-form" data-form-nonce="9d725a0f2ec9cef3ada60ee7c58b904f69bd9c48" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="6vvUk3MD/UKNYhcM2UlzxSnoGhFrF5lJ1D84/j1AEu6xKycQAJDZC0iLYGP8Q4AMZjAyg7dnlTRJboff0LQrLg==" /></div>
          <svg aria-hidden="true" class="octicon octicon-git-branch select-menu-item-icon" height="16" version="1.1" viewBox="0 0 10 16" width="10"><path d="M10 5c0-1.11-.89-2-2-2a1.993 1.993 0 0 0-1 3.72v.3c-.02.52-.23.98-.63 1.38-.4.4-.86.61-1.38.63-.83.02-1.48.16-2 .45V4.72a1.993 1.993 0 0 0-1-3.72C.88 1 0 1.89 0 3a2 2 0 0 0 1 1.72v6.56c-.59.35-1 .99-1 1.72 0 1.11.89 2 2 2 1.11 0 2-.89 2-2 0-.53-.2-1-.53-1.36.09-.06.48-.41.59-.47.25-.11.56-.17.94-.17 1.05-.05 1.95-.45 2.75-1.25S8.95 7.77 9 6.73h-.02C9.59 6.37 10 5.73 10 5zM2 1.8c.66 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2C1.35 4.2.8 3.65.8 3c0-.65.55-1.2 1.2-1.2zm0 12.41c-.66 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2zm6-8c-.66 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2z"></path></svg>
            <div class="select-menu-item-text">
              <span class="select-menu-item-heading">Create branch: <span class="js-new-item-name"></span></span>
              <span class="description">from ‘master’</span>
            </div>
            <input type="hidden" name="name" id="name" class="js-new-item-value">
            <input type="hidden" name="branch" id="branch" value="master">
            <input type="hidden" name="path" id="path" value="services/mobileaccess/google-auth-ios-swift-sdk.md">
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
    <span class="repo-root js-repo-root"><span class="js-path-segment"><a href="/IBM-Bluemix/docs-staging"><span>docs-staging</span></a></span></span><span class="separator">/</span><span class="js-path-segment"><a href="/IBM-Bluemix/docs-staging/tree/master/services"><span>services</span></a></span><span class="separator">/</span><span class="js-path-segment"><a href="/IBM-Bluemix/docs-staging/tree/master/services/mobileaccess"><span>mobileaccess</span></a></span><span class="separator">/</span><strong class="final-path">google-auth-ios-swift-sdk.md</strong>
  </div>
</div>

<include-fragment class="commit-tease" src="/IBM-Bluemix/docs-staging/contributors/master/services/mobileaccess/google-auth-ios-swift-sdk.md">
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
      <a href="/IBM-Bluemix/docs-staging/raw/master/services/mobileaccess/google-auth-ios-swift-sdk.md" class="btn btn-sm " id="raw-url">Raw</a>
        <a href="/IBM-Bluemix/docs-staging/blame/master/services/mobileaccess/google-auth-ios-swift-sdk.md" class="btn btn-sm js-update-url-with-hash">Blame</a>
      <a href="/IBM-Bluemix/docs-staging/commits/master/services/mobileaccess/google-auth-ios-swift-sdk.md" class="btn btn-sm " rel="nofollow">History</a>
    </div>

        <a class="btn-octicon tooltipped tooltipped-nw"
           href="github-windows://openRepo/https://github.com/IBM-Bluemix/docs-staging?branch=master&amp;filepath=services%2Fmobileaccess%2Fgoogle-auth-ios-swift-sdk.md"
           aria-label="Open this file in GitHub Desktop"
           data-ga-click="Repository, open with desktop, type:windows">
            <svg aria-hidden="true" class="octicon octicon-device-desktop" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M15 2H1c-.55 0-1 .45-1 1v9c0 .55.45 1 1 1h5.34c-.25.61-.86 1.39-2.34 2h8c-1.48-.61-2.09-1.39-2.34-2H15c.55 0 1-.45 1-1V3c0-.55-.45-1-1-1zm0 9H1V3h14v8z"></path></svg>
        </a>

        <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/IBM-Bluemix/docs-staging/edit/master/services/mobileaccess/google-auth-ios-swift-sdk.md" class="inline-form js-update-url-with-hash" data-form-nonce="9d725a0f2ec9cef3ada60ee7c58b904f69bd9c48" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="zSLQiJFIPJBt3FRwLA9WVfSauvNqbdNgbZoxoXskWn/hs20Q+rxPFfscaixmar1sye2fr/r33cDlHIs48b9rpw==" /></div>
          <button class="btn-octicon tooltipped tooltipped-nw" type="submit"
            aria-label="Edit this file" data-hotkey="e" data-disable-with>
            <svg aria-hidden="true" class="octicon octicon-pencil" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path d="M0 12v3h3l8-8-3-3-8 8zm3 2H1v-2h1v1h1v1zm10.3-9.3L12 6 9 3l1.3-1.3a.996.996 0 0 1 1.41 0l1.59 1.59c.39.39.39 1.02 0 1.41z"></path></svg>
          </button>
</form>        <!-- </textarea> --><!-- '"` --><form accept-charset="UTF-8" action="/IBM-Bluemix/docs-staging/delete/master/services/mobileaccess/google-auth-ios-swift-sdk.md" class="inline-form" data-form-nonce="9d725a0f2ec9cef3ada60ee7c58b904f69bd9c48" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="EQKpW3Z5XM7TsHIIJpXUde9xbdTSfBH2NscK6Ea4kktSkvFI/GqLKmltkIGILqPhLq5pPkIgPcDqqvfFJQ3wXA==" /></div>
          <button class="btn-octicon btn-octicon-danger tooltipped tooltipped-nw" type="submit"
            aria-label="Delete this file" data-disable-with>
            <svg aria-hidden="true" class="octicon octicon-trashcan" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path d="M11 2H9c0-.55-.45-1-1-1H5c-.55 0-1 .45-1 1H2c-.55 0-1 .45-1 1v1c0 .55.45 1 1 1v9c0 .55.45 1 1 1h7c.55 0 1-.45 1-1V5c.55 0 1-.45 1-1V3c0-.55-.45-1-1-1zm-1 12H3V5h1v8h1V5h1v8h1V5h1v8h1V5h1v9zm1-10H2V3h9v1z"></path></svg>
          </button>
</form>  </div>

  <div class="file-info">
      225 lines (144 sloc)
      <span class="file-info-divider"></span>
    11 KB
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
  <td><div>2016</div></td>
  </tr>
  </tbody>
</table></div></td>
  </tr>
  </tbody>
</table>

<p>{:screen:  .screen}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}</p>

<h1><a id="user-content-enabling-google-authentication-for-ios-apps-swift-sdk" class="anchor" href="#enabling-google-authentication-for-ios-apps-swift-sdk" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Enabling Google authentication for iOS apps (Swift SDK)</h1>

<p>{: #google-auth-ios}</p>

<p><em>Last updated: 17 July 2016</em>
{: .last-updated}</p>

<p>Use Google Sign-In to authenticate users on your {{site.data.keyword.amashort}} iOS Swift app. The newly released {{site.data.keyword.amashort}} Swift SDK  adds to and improves the functionality provided by the existing Mobile Client Access Objective-C SDK.</p>

<p><strong>Note:</strong> While the Objective-C SDK remains fully supported, and is still considered the primary SDK for  {{site.data.keyword.Bluemix_notm}} Mobile Services, there are plans to discontinue the Objective-C SDK later this year in favor of this new Swift SDK.</p>

<h2><a id="user-content-before-you-begin" class="anchor" href="#before-you-begin" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Before you begin</h2>

<p>{: #google-auth-ios-before}
You must have:</p>

<ul>
<li>An iOS project in Xcode. It does not need to be instrumented with the {{site.data.keyword.amashort}} client SDK.<br></li>
<li>An instance of a  {{site.data.keyword.Bluemix_notm}} application that is protected by {{site.data.keyword.amashort}} service. For more information about how to create a {{site.data.keyword.Bluemix_notm}} back-end application, see <a href="/IBM-Bluemix/docs-staging/blob/master/services/mobileaccess/index.html">Getting started</a>.</li>
</ul>

<h2><a id="user-content-preparing-your-app-for-google-sign-in" class="anchor" href="#preparing-your-app-for-google-sign-in" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Preparing your app for Google Sign-In</h2>

<p>{: #google-sign-in-ios}</p>

<p>Prepare your app for Google sign-in by following the instructions provided by Google at <a href="https://developers.google.com/identity/sign-in/ios/start-integrating">Google Sign-In for iOS</a>. </p>

<p>This process:</p>

<ul>
<li>prepares a new project on the Google Developers site, </li>
<li>creates the <code>GoogleService-Info.plist</code> file and the <code>REVERSE_CLIENT_ID</code> value to add to your Xcode project, and</li>
<li>creates the <strong>Google Client ID</strong> to add to your {{site.data.keyword.Bluemix_notm}} back-end application.</li>
</ul>

<p>The following steps give you a brief outline of the tasks necessary for preparing your app. </p>

<p><strong>Note:</strong> It is not necessary to add the <code>Google/SignIn</code> CocoaPod. The necessary SDK is added by the <code>BMSGoogleAuthentication</code> CocoaPod below.</p>

<ol>
<li><p>Note the <strong>Bundle Identifier</strong> in your Xcode project from the <strong>Identity</strong> section of the <strong>General</strong> tab of the main target. You need it to create your  Google Sign-In project.</p></li>
<li><p>Create a project on Google Developer for Google Sign-In for iOS at <a href="https://developers.google.com/mobile/add?platform=ios">https://developers.google.com/mobile/add?platform=ios</a>. </p></li>
<li><p>Add the Google Sign-In service to your project.</p></li>
<li><p>Retrieve the <code>GoogleService-Info.plist</code>.</p>

<p><strong>Important:</strong> When you get the <code>GoogleService-Info.plist</code> file, open it and note the <code>CLIENT_ID</code> value. You need this value later to configure {{site.data.keyword.amashort}} back-end application.</p></li>
<li><p>Add the <code>GoogleService-Info.plist</code> file to your Xcode project. For more information, see <a href="https://developers.google.com/identity/sign-in/ios/start-integrating#add-config">Add the configuration file to your project</a>.</p></li>
<li><p>Update the URL Schemes in your Xcode project with your <code>REVERSE_CLIENT_ID</code> and bundle identifier. For more information, see <a href="https://developers.google.com/identity/sign-in/ios/start-integrating#add_a_url_scheme_to_your_project">Add URL schemes to your project</a>.</p></li>
<li><p>Update your app's project-Bridging-Header.h file with the following code:</p>

<pre><code>#import &lt;Google/SignIn.h&gt;
</code></pre>

<p>For more information about updating the bridging header file, see step 1. in <a href="https://developers.google.com/identity/sign-in/ios/sign-in#enable_sign-in">Enable sign-in</a>.</p></li>
</ol>

<h2><a id="user-content-configuring-sitedatakeywordamashort-for-google-authentication" class="anchor" href="#configuring-sitedatakeywordamashort-for-google-authentication" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Configuring {{site.data.keyword.amashort}} for Google authentication</h2>

<p>{: #google-auth-ios-config}</p>

<p>Now that you have an iOS client ID, you can enable Google authentication in the {{site.data.keyword.Bluemix}} dashboard.</p>

<ol>
<li><p>Open your app in the {{site.data.keyword.Bluemix_notm}} dashboard.</p></li>
<li><p>Click <strong>Mobile Options</strong> and take note of <strong>Route</strong> (<em>applicationRoute</em>) and <strong>App GUID</strong> (<em>applicationGUID</em>). You need these values when you initialize the SDK.</p></li>
<li><p>Click the {{site.data.keyword.amashort}} tile. The {{site.data.keyword.amashort}} dashboard loads.</p></li>
<li><p>Click the <strong>Configure* button on the  **Google</strong> panel.</p></li>
<li><p>In <strong>Application ID for iOS</strong>, specify the <code>CLIENT_ID</code> value from the <code>GoogleService-Info.plist</code> file that you obtained earlier and click <strong>Save</strong>.</p></li>
</ol>

<h2><a id="user-content-configuring-the-sitedatakeywordamashort-client-sdk-for-ios" class="anchor" href="#configuring-the-sitedatakeywordamashort-client-sdk-for-ios" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Configuring the {{site.data.keyword.amashort}} client SDK for iOS</h2>

<p>{: #google-auth-ios-sdk}</p>

<h3><a id="user-content-installing-cocoapods" class="anchor" href="#installing-cocoapods" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Installing CocoaPods</h3>

<p>{: #install-cocoapods}</p>

<ol>
<li><p>Open Terminal and run the <strong>pod --version</strong> command. If you already have CocoaPods installed, the version number displays. You can skip to the next section to install the SDK.</p></li>
<li><p>If you do not have CocoaPods installed, run:</p></li>
</ol>

<pre><code>sudo gem install cocoapods
</code></pre>

<p>For more information, see the <a href="https://cocoapods.org/">CocoaPods website</a>.</p>

<h3><a id="user-content-installing-the-sitedatakeywordamashort-client-swift-sdk-with-cocoapods" class="anchor" href="#installing-the-sitedatakeywordamashort-client-swift-sdk-with-cocoapods" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Installing the {{site.data.keyword.amashort}} client Swift SDK with CocoaPods</h3>

<p>{: #facebook-auth-install-swift-cocoapods}</p>

<ol>
<li><p>If you have no <code>Podfile</code> in your iOS project, run <code>pod init</code> to create the file.</p></li>
<li><p>Edit the <code>Podfile</code> and add the following lines to the relevant target:</p>

<pre><code>use_frameworks!
pod 'BMSGoogleAuthentication'
</code></pre>

<p><strong>Note:</strong> If you have already installed the {{site.data.keyword.amashort}} core SDK, you can remove this line: <code>pod 'BMSSecurity'</code>. The <code>BMSGoogleAuthentication</code> pod installs all necessary frameworks.</p>

<p><strong>Tip:</strong> You can add <code>use_frameworks!</code> to your Xcode target instead of having it in the Podfile.</p></li>
<li><p>Save the <code>Podfile</code> and run <code>pod install</code> from the command line. CocoaPods  installs the dependencies. You will see the progress and which components were added.</p>

<p><strong>Important</strong>: You now must open your project by using the <code>xcworkspace</code> file that is generated by CocoaPods. Usually the name is <code>{your-project-name}.xcworkspace</code>.  </p></li>
<li><p>Run <code>open {your-project-name}.xcworkspace</code> from the command line to open your iOS project workspace.</p></li>
<li><p>Copy the <code>GoogleAuthenticationManager.swift</code> file from the <code>BMSGoogleAuthentication</code> pod source files to your project directory.</p></li>
</ol>

<h2><a id="user-content-initializing-the-sitedatakeywordamashort-client-swift-sdk" class="anchor" href="#initializing-the-sitedatakeywordamashort-client-swift-sdk" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Initializing the {{site.data.keyword.amashort}} client Swift SDK</h2>

<p>{: #google-auth-ios-initialize}</p>

<p>To use the {{site.data.keyword.amashort}} client SDK,  initialize it by passing the <code>applicationGUID</code>, and <code>applicationRoute</code> parameters.</p>

<p>A common, though not mandatory, place to put the initialization code is in the <code>application:didFinishLaunchingWithOptions</code> method of your application delegate.</p>

<ol>
<li><p>Get your application parameter values. Open your app in the {{site.data.keyword.Bluemix_notm}} dashboard. Click <strong>Mobile Options</strong>. The <code>applicationRoute</code> and <code>applicationGUID</code> values are displayed in the <strong>Route</strong> and <strong>App GUID</strong> fields.</p></li>
<li><p>Import the required frameworks in the class where you want to use the {{site.data.keyword.amashort}} client SDK. Add the following headers:</p>

<div class="highlight highlight-source-swift"><pre><span class="pl-k">import</span> <span class="pl-c1">UIKit</span>
<span class="pl-k">import</span> <span class="pl-c1">BMSCore</span>
<span class="pl-k">import</span> <span class="pl-c1">BMSSecurity</span></pre></div></li>
<li><p>Use the following code to initialize the client SDK. Replace <code>&lt;applicationRoute&gt;</code> and <code>&lt;applicationGUID&gt;</code> with values for <strong>Route</strong> and <strong>App GUID</strong> that you obtained from <strong>Mobile Options</strong> in the {{site.data.keyword.Bluemix_notm}} dashboard. Replace <code>&lt;applicationBluemixRegion&gt;</code> with the region where your {{site.data.keyword.Bluemix_notm}} application is hosted. To view your {{site.data.keyword.Bluemix_notm}} region, click on the face icon (<a href="/IBM-Bluemix/docs-staging/blob/master/face.png" target="_blank"><img src="/IBM-Bluemix/docs-staging/raw/master/face.png" alt="Face" title="Face" style="max-width:100%;"></a>) in the upper-left corner of the dashboard. </p>

<div class="highlight highlight-source-swift"><pre><span class="pl-k">let</span> backendURL <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">"</span>&lt;applicationRoute&gt;<span class="pl-pds">"</span></span>
<span class="pl-k">let</span> backendGUID <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">"</span>&lt;applicationGUID&gt;<span class="pl-pds">"</span></span>

<span class="pl-k">func</span> <span class="pl-en">application</span>(application: UIApplication, <span class="pl-en">didFinishLaunchingWithOptions</span> <span class="pl-smi">launchOptions</span>: [NSObject: <span class="pl-c1">AnyObject</span>]?) <span class="pl-k">-&gt;</span> <span class="pl-c1">Bool</span> {

<span class="pl-c">// Initialize the client SDK.  </span>
BMSClient<span class="pl-k">.</span>sharedInstance<span class="pl-k">.</span>initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUId, bluemixRegion: BMSClient<span class="pl-k">.&lt;</span>applicationBluemixRegion<span class="pl-k">&gt;</span>)

BMSClient<span class="pl-k">.</span>sharedInstance<span class="pl-k">.</span>authorizationManager <span class="pl-k">=</span> MCAAuthorizationManager<span class="pl-k">.</span>sharedInstance

GoogleAuthenticationManager<span class="pl-k">.</span>sharedInstance<span class="pl-k">.</span>register()
    <span class="pl-k">return</span> <span class="pl-c1">true</span>
    }

<span class="pl-c">// [START openurl]</span>
    <span class="pl-k">func</span> <span class="pl-en">application</span>(application: UIApplication,
        <span class="pl-en">openURL</span> <span class="pl-smi">url</span>: NSURL, sourceApplication: <span class="pl-c1">String</span>?, annotation: <span class="pl-c1">AnyObject</span>) <span class="pl-k">-&gt;</span> <span class="pl-c1">Bool</span> {
           <span class="pl-k">return</span> GoogleAuthenticationManager<span class="pl-k">.</span>sharedInstance<span class="pl-k">.</span>handleApplicationOpenUrl(openURL: url, sourceApplication: sourceApplication, annotation: annotation)
    }

<span class="pl-k">@available</span>(iOS <span class="pl-c1">9</span><span class="pl-k">.</span><span class="pl-c1">0</span>, <span class="pl-k">*</span>)
<span class="pl-k">func</span> <span class="pl-en">application</span>(app: UIApplication, <span class="pl-en">openURL</span> <span class="pl-smi">url</span>: NSURL, options: [<span class="pl-c1">String</span> <span class="pl-k">:</span> <span class="pl-c1">AnyObject</span>]) <span class="pl-k">-&gt;</span> <span class="pl-c1">Bool</span> {
<span class="pl-k">return</span> GoogleAuthenticationManager<span class="pl-k">.</span>sharedInstance<span class="pl-k">.</span>handleApplicationOpenUrl(openURL: url, options: options)
}</pre></div></li>
</ol>

<h2><a id="user-content-testing-the-authentication" class="anchor" href="#testing-the-authentication" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Testing the authentication</h2>

<p>{: #google-auth-ios-testing}</p>

<p>After the client SDK is initialized and Google Authentication Manager is registered, you can start making requests to your mobile back-end application.</p>

<h3><a id="user-content-before-you-begin-1" class="anchor" href="#before-you-begin-1" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Before you begin</h3>

<p>{: #google-auth-ios-testing-before}</p>

<p>You must be using the {{site.data.keyword.mobilefirstbp}}  boilerplate and already have a resource protected by {{site.data.keyword.amashort}} at the <code>/protected</code> endpoint. If you need to set up a <code>/protected</code> endpoint, see <a href="https://console.%7BDomainName%7D/docs/services/mobileaccess/protecting-resources.html">Protecting resources</a>.</p>

<ol>
<li><p>Try to send a request to protected endpoint of your mobile back-end application in your desktop browser by opening <code>{applicationRoute}/protected</code>, for example <code>http://my-mobile-backend.mybluemix.net/protected</code></p></li>
<li><p>The <code>/protected</code> endpoint of a mobile back-end application created with MobileFirst Services Boilerplate is protected with {{site.data.keyword.amashort}}, therefore it can only be accessed by mobile applications instrumented with {{site.data.keyword.amashort}} client SDK. As a result you will see <code>Unauthorized</code> in your desktop browser.</p></li>
<li><p>Use your iOS application to make request to the same endpoint.</p>

<div class="highlight highlight-source-swift"><pre><span class="pl-k">let</span> protectedResourceURL <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">"</span>&lt;Your protected resource URL&gt;<span class="pl-pds">"</span></span> <span class="pl-c">// any protected resource</span>
<span class="pl-k">let</span> request <span class="pl-k">=</span> Request(url: protectedResourceURL , method: HttpMethod<span class="pl-k">.</span>GET)
<span class="pl-k">let</span> callBack:BmsCompletionHandler <span class="pl-k">=</span> {(response: Response?, error: NSError?) <span class="pl-k">in</span>
<span class="pl-k">if</span> error <span class="pl-k">==</span> <span class="pl-c1">nil</span> {
  <span class="pl-c1">print</span> (<span class="pl-s"><span class="pl-pds">"</span>response:<span class="pl-pse">\(</span><span class="pl-s1">response?<span class="pl-k">.</span>responseText</span><span class="pl-pse">)</span>, no error<span class="pl-pds">"</span></span>)
} <span class="pl-k">else</span> {
  <span class="pl-c1">print</span> (<span class="pl-s"><span class="pl-pds">"</span>error: <span class="pl-pse">\(</span><span class="pl-s1">error</span><span class="pl-pse">)</span><span class="pl-pds">"</span></span>)
}
}

request<span class="pl-k">.</span>sendWithCompletionHandler(callBack)</pre></div></li>
<li><p>Run your application. You will see a Google Login screen pop-up</p>

<p><a href="/IBM-Bluemix/docs-staging/blob/master/services/mobileaccess/images/ios-google-login.png" target="_blank"><img src="/IBM-Bluemix/docs-staging/raw/master/services/mobileaccess/images/ios-google-login.png" alt="image" style="max-width:100%;"></a></p></li>
<li><p>When you log in and click <strong>OK</strong>, you're authorizing {{site.data.keyword.amashort}} to use your Google user identity for authentication purposes.</p></li>
<li><p>Your request should succeed. The following output appears in the log.</p>

<pre><code>onAuthenticationSuccess info = Optional({attributes = {};
   deviceId = 105747725068605084657;
   displayName = "donlonqwerty@gmail.com";
   isUserAuthenticated = 1;
   userId = 105747725068605084657;
})
response:Optional("Hello, this is a protected resource!"), no error
</code></pre>

<p>{: screen}</p></li>
<li><p>You can also add logout functionality by adding the following code:</p>

<pre><code>GoogleAuthenticationManager.sharedInstance.logout(callBack)
</code></pre>

<p>If you call this code after a user is logged in with Google and the user tries to log in again, they are prompted to authorize {{site.data.keyword.amashort}} to use Google for authentication purposes. At that point, the user can click the user name in the upper-right corner of the screen to select and log in with another user.</p>

<p>Passing <code>callBack</code> to the logout function is optional. You can also pass <code>nil</code>.</p></li>
</ol>
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
      <li>&copy; 2016 <span title="0.14656s from github-fe124-cp1-prd.iad.github.net">GitHub</span>, Inc.</li>
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

