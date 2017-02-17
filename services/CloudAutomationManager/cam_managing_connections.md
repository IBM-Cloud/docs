





<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">

<meta content="origin-when-cross-origin" name="referrer" />

  <link crossorigin="anonymous" href="https://assets-cdn.github.com/assets/frameworks-d311c4a37b4a480a760dda55c72eb656b70f39154f15e1b7a7f6506e143d7ec0.css" integrity="sha256-0xHEo3tKSAp2DdpVxy62VrcPORVPFeG3p/ZQbhQ9fsA=" media="all" rel="stylesheet" />
  <link crossorigin="anonymous" href="https://assets-cdn.github.com/assets/github-5f9b35cedfc79777aca47137798257f30e25a604574d53e002ae26b3c9930bf7.css" integrity="sha256-X5s1zt/Hl3espHE3eYJX8w4lpgRXTVPgAq4ms8mTC/c=" media="all" rel="stylesheet" />
  
  
  
  

  <meta name="viewport" content="width=device-width">
  
  <title>docs-staging/cam_managing_connections.md at master · IBM-Bluemix/docs-staging</title>
  <link rel="search" type="application/opensearchdescription+xml" href="/opensearch.xml" title="GitHub">
  <link rel="fluid-icon" href="https://github.com/fluidicon.png" title="GitHub">
  <meta property="fb:app_id" content="1401488693436528">


  <link rel="assets" href="https://assets-cdn.github.com/">
  <link rel="web-socket" href="wss://live.github.com/_sockets/VjI6MTU0NTc0ODgwOjM3MjAzNGQwMGU1ODMwZjE1NDM5MmMyMzFiYmYzY2EyZmMwMDc2Y2MzMzljOGViMTgwNDhmYWI0MDE5MWEyYTk=--1a6330e3b50c1feae77ae055da08cddb1d419016">
  <meta name="pjax-timeout" content="1000">
  <link rel="sudo-modal" href="/sessions/sudo_modal">
  <meta name="request-id" content="F619:294CA:6B5CC8:AD67D1:58A6CEFD" data-pjax-transient>
  

  <meta name="selected-link" value="repo_source" data-pjax-transient>

  <meta name="google-site-verification" content="KT5gs8h0wvaagLKAVWq8bbeNwnZZK1r1XQysX3xurLU">
<meta name="google-site-verification" content="ZzhVyEFwb7w3e0-uOTltm8Jsck2F5StVihD0exw2fsA">
    <meta name="google-analytics" content="UA-3769691-2">

<meta content="collector.githubapp.com" name="octolytics-host" /><meta content="github" name="octolytics-app-id" /><meta content="https://collector.githubapp.com/github-external/browser_event" name="octolytics-event-url" /><meta content="F619:294CA:6B5CC8:AD67D1:58A6CEFD" name="octolytics-dimension-request_id" /><meta content="20184013" name="octolytics-actor-id" /><meta content="gcatasta" name="octolytics-actor-login" /><meta content="dbfe320a4801ce7d3f69a6fc7da126c7b9aa45836cd55a9a1dc70e0fe8e9f6f5" name="octolytics-actor-hash" />
<meta content="/&lt;user-name&gt;/&lt;repo-name&gt;/blob/show" data-pjax-transient="true" name="analytics-location" />



  <meta class="js-ga-set" name="dimension1" content="Logged In">



      <meta name="hostname" content="github.com">
  <meta name="user-login" content="gcatasta">

      <meta name="expected-hostname" content="github.com">
    <meta name="js-proxy-site-detection-payload" content="YzRiMGIyODY3MzUyNGJlNzE5ZjU3Y2E3NjZlYzIwMzg0NDg4ZDFiOTEwNmQwYmMyNTA3MjU3MDAzNDRjYTk0Ynx7InJlbW90ZV9hZGRyZXNzIjoiMTk1LjIxMi4yOS4xODUiLCJyZXF1ZXN0X2lkIjoiRjYxOToyOTRDQTo2QjVDQzg6QUQ2N0QxOjU4QTZDRUZEIiwidGltZXN0YW1wIjoxNDg3MzI2OTc0LCJob3N0IjoiZ2l0aHViLmNvbSJ9">


  <meta name="html-safe-nonce" content="884d373e7d34e868cdc1df3b1a7dbc6d3de8b5c0">

  <meta http-equiv="x-pjax-version" content="23929be193bd223d06c6c0868f90d120">
  

    
  <meta name="description" content="docs-staging - IBM Bluemix documentation on the staging app.">
  <meta name="go-import" content="github.com/IBM-Bluemix/docs-staging git https://github.com/IBM-Bluemix/docs-staging.git">

  <meta content="7284885" name="octolytics-dimension-user_id" /><meta content="IBM-Bluemix" name="octolytics-dimension-user_login" /><meta content="39894162" name="octolytics-dimension-repository_id" /><meta content="IBM-Bluemix/docs-staging" name="octolytics-dimension-repository_nwo" /><meta content="false" name="octolytics-dimension-repository_public" /><meta content="false" name="octolytics-dimension-repository_is_fork" /><meta content="39894162" name="octolytics-dimension-repository_network_root_id" /><meta content="IBM-Bluemix/docs-staging" name="octolytics-dimension-repository_network_root_nwo" />
  <link href="https://github.com/IBM-Bluemix/docs-staging/commits/master.atom?token=ATP7zUcE5myCLs50ekL8cq6R17uovjhMks62sq_-wA%3D%3D" rel="alternate" title="Recent Commits to docs-staging:master" type="application/atom+xml">


    <link rel="canonical" href="https://github.com/IBM-Bluemix/docs-staging/blob/master/services/CloudAutomationManager/cam_managing_connections.md" data-pjax-transient>


  <meta name="browser-stats-url" content="https://api.github.com/_private/browser/stats">

  <meta name="browser-errors-url" content="https://api.github.com/_private/browser/errors">

  <link rel="mask-icon" href="https://assets-cdn.github.com/pinned-octocat.svg" color="#000000">
  <link rel="icon" type="image/x-icon" href="https://assets-cdn.github.com/favicon.ico">

<meta name="theme-color" content="#1e2327">



  </head>

  <body class="logged-in env-production windows vis-private page-blob">
    

  <div class="position-relative js-header-wrapper ">
    <a href="#start-of-content" tabindex="1" class="accessibility-aid js-skip-to-content">Skip to content</a>
    <div id="js-pjax-loader-bar" class="pjax-loader-bar"><div class="progress"></div></div>

    
    
    



        <div class="header" role="banner">
  <div class="container clearfix">

    <a class="header-logo-invertocat" href="https://github.com/" data-hotkey="g d" aria-label="Homepage" data-ga-click="Header, go to dashboard, icon:logo">
  <svg aria-hidden="true" class="octicon octicon-mark-github" height="32" version="1.1" viewBox="0 0 16 16" width="32"><path fill-rule="evenodd" d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0 0 16 8c0-4.42-3.58-8-8-8z"/></svg>
</a>


        <div class="header-search scoped-search site-scoped-search js-site-search" role="search">
  <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/IBM-Bluemix/docs-staging/search" class="js-site-search-form" data-scoped-search-url="/IBM-Bluemix/docs-staging/search" data-unscoped-search-url="/search" method="get"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /></div>
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
        autocapitalize="off">
    </label>
</form></div>


      <ul class="header-nav float-left" role="navigation">
        <li class="header-nav-item">
          <a href="/pulls" aria-label="Pull requests you created" class="js-selected-navigation-item header-nav-link" data-ga-click="Header, click, Nav menu - item:pulls context:user" data-hotkey="g p" data-selected-links="/pulls /pulls/assigned /pulls/mentioned /pulls">
            Pull requests
</a>        </li>
        <li class="header-nav-item">
          <a href="/issues" aria-label="Issues you created" class="js-selected-navigation-item header-nav-link" data-ga-click="Header, click, Nav menu - item:issues context:user" data-hotkey="g i" data-selected-links="/issues /issues/assigned /issues/mentioned /issues">
            Issues
</a>        </li>
          <li class="header-nav-item">
            <a class="header-nav-link" href="https://gist.github.com/" data-ga-click="Header, go to gist, text:gist">Gist</a>
          </li>
      </ul>

    
<ul class="header-nav user-nav float-right" id="user-links">
  <li class="header-nav-item">
    

  </li>

  <li class="header-nav-item dropdown js-menu-container">
    <a class="header-nav-link tooltipped tooltipped-s js-menu-target" href="/new"
       aria-label="Create new…"
       data-ga-click="Header, create new, icon:add">
      <svg aria-hidden="true" class="octicon octicon-plus float-left" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 9H7v5H5V9H0V7h5V2h2v5h5z"/></svg>
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

<a class="dropdown-item" href="https://gist.github.com/" data-ga-click="Header, create new gist">
  New gist
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
    <a class="header-nav-link name tooltipped tooltipped-sw js-menu-target" href="/gcatasta"
       aria-label="View profile and more"
       data-ga-click="Header, show menu, icon:avatar">
      <img alt="@gcatasta" class="avatar" height="20" src="https://avatars2.githubusercontent.com/u/20184013?v=3&amp;s=40" width="20" />
      <span class="dropdown-caret"></span>
    </a>

    <div class="dropdown-menu-content js-menu-content">
      <div class="dropdown-menu dropdown-menu-sw">
        <div class="dropdown-header header-nav-current-user css-truncate">
          Signed in as <strong class="css-truncate-target">gcatasta</strong>
        </div>

        <div class="dropdown-divider"></div>

        <a class="dropdown-item" href="/gcatasta" data-ga-click="Header, go to profile, text:your profile">
          Your profile
        </a>
        <a class="dropdown-item" href="/gcatasta?tab=stars" data-ga-click="Header, go to starred repos, text:your stars">
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

        <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/logout" class="logout-form" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="Oe1rvNwRdOd3Cex5EU+k+Ig9Z2O22ZRm9mXOE4fSDqOKBUxBUeGC1gqRg8Fcw7q385To0T1E1XnWAdMTKWSobg==" /></div>
          <button type="submit" class="dropdown-item dropdown-signout" data-ga-click="Header, sign out, icon:logout">
            Sign out
          </button>
</form>      </div>
    </div>
  </li>
</ul>

    <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/logout" class="sr-only" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="ShkSEKmviaEwPxn6CxU5Cznfs9NXC1I9qI2Rum58Qy758TXtJF9/kE2ndkJGmSdEQnY8YdyWEyKI6Yy6wMrl4w==" /></div>
      <button type="submit" class="dropdown-item dropdown-signout" data-ga-click="Header, sign out, icon:logout">
        Sign out
      </button>
</form>
    
  </div>
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
        <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/notifications/subscribe" class="js-social-container" data-autosubmit="true" data-remote="true" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="d1GbIxGI4P8i9hB3CZFjAAdjT/3TTE8nTWLLjvcLwBCST2gjNrDB2yohmyaJKR8giNibD0zeqtlzUGPCY8ZnIA==" /></div>      <input class="form-control" id="repository_id" name="repository_id" type="hidden" value="39894162" />

        <div class="select-menu js-menu-container js-select-menu">
          <a href="/IBM-Bluemix/docs-staging/subscription"
            class="btn btn-sm btn-with-count select-menu-button js-menu-target" role="button" tabindex="0" aria-haspopup="true"
            data-ga-click="Repository, click Watch settings, action:blob#show">
            <span class="js-select-button">
              <svg aria-hidden="true" class="octicon octicon-eye" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M8.06 2C3 2 0 8 0 8s3 6 8.06 6C13 14 16 8 16 8s-3-6-7.94-6zM8 12c-2.2 0-4-1.78-4-4 0-2.2 1.8-4 4-4 2.22 0 4 1.8 4 4 0 2.22-1.78 4-4 4zm2-4c0 1.11-.89 2-2 2-1.11 0-2-.89-2-2 0-1.11.89-2 2-2 1.11 0 2 .89 2 2z"/></svg>
              Watch
            </span>
          </a>
          <a class="social-count js-social-count"
            href="/IBM-Bluemix/docs-staging/watchers"
            aria-label="84 users are watching this repository">
            84
          </a>

        <div class="select-menu-modal-holder">
          <div class="select-menu-modal subscription-menu-modal js-menu-content" aria-hidden="true">
            <div class="select-menu-header js-navigation-enable" tabindex="-1">
              <svg aria-label="Close" class="octicon octicon-x js-menu-close" height="16" role="img" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M7.48 8l3.75 3.75-1.48 1.48L6 9.48l-3.75 3.75-1.48-1.48L4.52 8 .77 4.25l1.48-1.48L6 6.52l3.75-3.75 1.48 1.48z"/></svg>
              <span class="select-menu-title">Notifications</span>
            </div>

              <div class="select-menu-list js-navigation-container" role="menu">

                <div class="select-menu-item js-navigation-item selected" role="menuitem" tabindex="0">
                  <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
                  <div class="select-menu-item-text">
                    <input checked="checked" id="do_included" name="do" type="radio" value="included" />
                    <span class="select-menu-item-heading">Not watching</span>
                    <span class="description">Be notified when participating or @mentioned.</span>
                    <span class="js-select-button-text hidden-select-button-text">
                      <svg aria-hidden="true" class="octicon octicon-eye" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M8.06 2C3 2 0 8 0 8s3 6 8.06 6C13 14 16 8 16 8s-3-6-7.94-6zM8 12c-2.2 0-4-1.78-4-4 0-2.2 1.8-4 4-4 2.22 0 4 1.8 4 4 0 2.22-1.78 4-4 4zm2-4c0 1.11-.89 2-2 2-1.11 0-2-.89-2-2 0-1.11.89-2 2-2 1.11 0 2 .89 2 2z"/></svg>
                      Watch
                    </span>
                  </div>
                </div>

                <div class="select-menu-item js-navigation-item " role="menuitem" tabindex="0">
                  <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
                  <div class="select-menu-item-text">
                    <input id="do_subscribed" name="do" type="radio" value="subscribed" />
                    <span class="select-menu-item-heading">Watching</span>
                    <span class="description">Be notified of all conversations.</span>
                    <span class="js-select-button-text hidden-select-button-text">
                      <svg aria-hidden="true" class="octicon octicon-eye" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M8.06 2C3 2 0 8 0 8s3 6 8.06 6C13 14 16 8 16 8s-3-6-7.94-6zM8 12c-2.2 0-4-1.78-4-4 0-2.2 1.8-4 4-4 2.22 0 4 1.8 4 4 0 2.22-1.78 4-4 4zm2-4c0 1.11-.89 2-2 2-1.11 0-2-.89-2-2 0-1.11.89-2 2-2 1.11 0 2 .89 2 2z"/></svg>
                      Unwatch
                    </span>
                  </div>
                </div>

                <div class="select-menu-item js-navigation-item " role="menuitem" tabindex="0">
                  <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
                  <div class="select-menu-item-text">
                    <input id="do_ignore" name="do" type="radio" value="ignore" />
                    <span class="select-menu-item-heading">Ignoring</span>
                    <span class="description">Never be notified.</span>
                    <span class="js-select-button-text hidden-select-button-text">
                      <svg aria-hidden="true" class="octicon octicon-mute" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M8 2.81v10.38c0 .67-.81 1-1.28.53L3 10H1c-.55 0-1-.45-1-1V7c0-.55.45-1 1-1h2l3.72-3.72C7.19 1.81 8 2.14 8 2.81zm7.53 3.22l-1.06-1.06-1.97 1.97-1.97-1.97-1.06 1.06L11.44 8 9.47 9.97l1.06 1.06 1.97-1.97 1.97 1.97 1.06-1.06L13.56 8l1.97-1.97z"/></svg>
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
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/IBM-Bluemix/docs-staging/unstar" class="starred" data-remote="true" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="Yba/doWglfll9S9Qn78iy4GewmSim/a/Eklrhm5pGvMmLDLr4LtyG6tgWE4IwuRJ7Vq9gR60wTPdRKiqlkDU8Q==" /></div>
      <button
        type="submit"
        class="btn btn-sm btn-with-count js-toggler-target"
        aria-label="Unstar this repository" title="Unstar IBM-Bluemix/docs-staging"
        data-ga-click="Repository, click unstar button, action:blob#show; text:Unstar">
        <svg aria-hidden="true" class="octicon octicon-star" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path fill-rule="evenodd" d="M14 6l-4.9-.64L7 1 4.9 5.36 0 6l3.6 3.26L2.67 14 7 11.67 11.33 14l-.93-4.74z"/></svg>
        Unstar
      </button>
        <a class="social-count js-social-count" href="/IBM-Bluemix/docs-staging/stargazers"
           aria-label="9 users starred this repository">
          9
        </a>
</form>
    <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/IBM-Bluemix/docs-staging/star" class="unstarred" data-remote="true" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="6dLA2pjawDyl1Jp71Rj10Zmq+xlWE1Sd/4HD1mgZliRDH2NrhEfkMrRPdlSLhlZTMpFTKnQNZQQr7SjRWkIdaA==" /></div>
      <button
        type="submit"
        class="btn btn-sm btn-with-count js-toggler-target"
        aria-label="Star this repository" title="Star IBM-Bluemix/docs-staging"
        data-ga-click="Repository, click star button, action:blob#show; text:Star">
        <svg aria-hidden="true" class="octicon octicon-star" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path fill-rule="evenodd" d="M14 6l-4.9-.64L7 1 4.9 5.36 0 6l3.6 3.26L2.67 14 7 11.67 11.33 14l-.93-4.74z"/></svg>
        Star
      </button>
        <a class="social-count js-social-count" href="/IBM-Bluemix/docs-staging/stargazers"
           aria-label="9 users starred this repository">
          9
        </a>
</form>  </div>

  </li>

  <li>
          <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/IBM-Bluemix/docs-staging/fork" class="btn-with-count" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="Vg/c2fxNeovVmumWma6FnDVtsfcTPf9Q5d/7M0tNGYoFC9BFYT5UblUet0DQ2V0l/vN3ZzqMtUGpDCASeQunbg==" /></div>
            <button
                type="submit"
                class="btn btn-sm btn-with-count"
                data-ga-click="Repository, show fork modal, action:blob#show; text:Fork"
                title="Fork your own copy of IBM-Bluemix/docs-staging to your account"
                aria-label="Fork your own copy of IBM-Bluemix/docs-staging to your account">
              <svg aria-hidden="true" class="octicon octicon-repo-forked" height="16" version="1.1" viewBox="0 0 10 16" width="10"><path fill-rule="evenodd" d="M8 1a1.993 1.993 0 0 0-1 3.72V6L5 8 3 6V4.72A1.993 1.993 0 0 0 2 1a1.993 1.993 0 0 0-1 3.72V6.5l3 3v1.78A1.993 1.993 0 0 0 5 15a1.993 1.993 0 0 0 1-3.72V9.5l3-3V4.72A1.993 1.993 0 0 0 8 1zM2 4.2C1.34 4.2.8 3.65.8 3c0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2zm3 10c-.66 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2zm3-10c-.66 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2z"/></svg>
              Fork
            </button>
</form>
    <a href="/IBM-Bluemix/docs-staging/network" class="social-count"
       aria-label="56 users forked this repository">
      56
    </a>
  </li>
</ul>

    <h1 class="private ">
  <svg aria-hidden="true" class="octicon octicon-lock" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M4 13H3v-1h1v1zm8-6v7c0 .55-.45 1-1 1H1c-.55 0-1-.45-1-1V7c0-.55.45-1 1-1h1V4c0-2.2 1.8-4 4-4s4 1.8 4 4v2h1c.55 0 1 .45 1 1zM3.8 6h4.41V4c0-1.22-.98-2.2-2.2-2.2-1.22 0-2.2.98-2.2 2.2v2H3.8zM11 7H2v7h9V7zM4 8H3v1h1V8zm0 2H3v1h1v-1z"/></svg>
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
    <a href="/IBM-Bluemix/docs-staging" class="js-selected-navigation-item selected reponav-item" data-hotkey="g c" data-selected-links="repo_source repo_downloads repo_commits repo_releases repo_tags repo_branches /IBM-Bluemix/docs-staging" itemprop="url">
      <svg aria-hidden="true" class="octicon octicon-code" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path fill-rule="evenodd" d="M9.5 3L8 4.5 11.5 8 8 11.5 9.5 13 14 8 9.5 3zm-5 0L0 8l4.5 5L6 11.5 2.5 8 6 4.5 4.5 3z"/></svg>
      <span itemprop="name">Code</span>
      <meta itemprop="position" content="1">
</a>  </span>

    <span itemscope itemtype="http://schema.org/ListItem" itemprop="itemListElement">
      <a href="/IBM-Bluemix/docs-staging/issues" class="js-selected-navigation-item reponav-item" data-hotkey="g i" data-selected-links="repo_issues repo_labels repo_milestones /IBM-Bluemix/docs-staging/issues" itemprop="url">
        <svg aria-hidden="true" class="octicon octicon-issue-opened" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path fill-rule="evenodd" d="M7 2.3c3.14 0 5.7 2.56 5.7 5.7s-2.56 5.7-5.7 5.7A5.71 5.71 0 0 1 1.3 8c0-3.14 2.56-5.7 5.7-5.7zM7 1C3.14 1 0 4.14 0 8s3.14 7 7 7 7-3.14 7-7-3.14-7-7-7zm1 3H6v5h2V4zm0 6H6v2h2v-2z"/></svg>
        <span itemprop="name">Issues</span>
        <span class="counter">10</span>
        <meta itemprop="position" content="2">
</a>    </span>

  <span itemscope itemtype="http://schema.org/ListItem" itemprop="itemListElement">
    <a href="/IBM-Bluemix/docs-staging/pulls" class="js-selected-navigation-item reponav-item" data-hotkey="g p" data-selected-links="repo_pulls /IBM-Bluemix/docs-staging/pulls" itemprop="url">
      <svg aria-hidden="true" class="octicon octicon-git-pull-request" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M11 11.28V5c-.03-.78-.34-1.47-.94-2.06C9.46 2.35 8.78 2.03 8 2H7V0L4 3l3 3V4h1c.27.02.48.11.69.31.21.2.3.42.31.69v6.28A1.993 1.993 0 0 0 10 15a1.993 1.993 0 0 0 1-3.72zm-1 2.92c-.66 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2zM4 3c0-1.11-.89-2-2-2a1.993 1.993 0 0 0-1 3.72v6.56A1.993 1.993 0 0 0 2 15a1.993 1.993 0 0 0 1-3.72V4.72c.59-.34 1-.98 1-1.72zm-.8 10c0 .66-.55 1.2-1.2 1.2-.65 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2zM2 4.2C1.34 4.2.8 3.65.8 3c0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2z"/></svg>
      <span itemprop="name">Pull requests</span>
      <span class="counter">11</span>
      <meta itemprop="position" content="3">
</a>  </span>

  <a href="/IBM-Bluemix/docs-staging/projects" class="js-selected-navigation-item reponav-item" data-selected-links="repo_projects new_repo_project repo_project /IBM-Bluemix/docs-staging/projects">
    <svg aria-hidden="true" class="octicon octicon-project" height="16" version="1.1" viewBox="0 0 15 16" width="15"><path fill-rule="evenodd" d="M10 12h3V2h-3v10zm-4-2h3V2H6v8zm-4 4h3V2H2v12zm-1 1h13V1H1v14zM14 0H1a1 1 0 0 0-1 1v14a1 1 0 0 0 1 1h13a1 1 0 0 0 1-1V1a1 1 0 0 0-1-1z"/></svg>
    Projects
    <span class="counter">0</span>
</a>
    <a href="/IBM-Bluemix/docs-staging/wiki" class="js-selected-navigation-item reponav-item" data-hotkey="g w" data-selected-links="repo_wiki /IBM-Bluemix/docs-staging/wiki">
      <svg aria-hidden="true" class="octicon octicon-book" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M3 5h4v1H3V5zm0 3h4V7H3v1zm0 2h4V9H3v1zm11-5h-4v1h4V5zm0 2h-4v1h4V7zm0 2h-4v1h4V9zm2-6v9c0 .55-.45 1-1 1H9.5l-1 1-1-1H2c-.55 0-1-.45-1-1V3c0-.55.45-1 1-1h5.5l1 1 1-1H15c.55 0 1 .45 1 1zm-8 .5L7.5 3H2v9h6V3.5zm7-.5H9.5l-.5.5V12h6V3z"/></svg>
      Wiki
</a>

  <a href="/IBM-Bluemix/docs-staging/pulse" class="js-selected-navigation-item reponav-item" data-selected-links="pulse /IBM-Bluemix/docs-staging/pulse">
    <svg aria-hidden="true" class="octicon octicon-pulse" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path fill-rule="evenodd" d="M11.5 8L8.8 5.4 6.6 8.5 5.5 1.6 2.38 8H0v2h3.6l.9-1.8.9 5.4L9 8.5l1.6 1.5H14V8z"/></svg>
    Pulse
</a>
  <a href="/IBM-Bluemix/docs-staging/graphs" class="js-selected-navigation-item reponav-item" data-selected-links="repo_graphs repo_contributors /IBM-Bluemix/docs-staging/graphs">
    <svg aria-hidden="true" class="octicon octicon-graph" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M16 14v1H0V0h1v14h15zM5 13H3V8h2v5zm4 0H7V3h2v10zm4 0h-2V6h2v7z"/></svg>
    Graphs
</a>

</nav>

  </div>
</div>

<div class="container new-discussion-timeline experiment-repo-nav">
  <div class="repository-content">

    

<a href="/IBM-Bluemix/docs-staging/blob/10541b6d8b1c93934dc907791abc8f2fb94992a7/services/CloudAutomationManager/cam_managing_connections.md" class="d-none js-permalink-shortcut" data-hotkey="y">Permalink</a>

<!-- blob contrib key: blob_contributors:v21:17d85b88ea040793ab5bd0561e651e37 -->

<div class="file-navigation js-zeroclipboard-container">
  
<div class="select-menu branch-select-menu js-menu-container js-select-menu float-left">
  <button class="btn btn-sm select-menu-button js-menu-target css-truncate" data-hotkey="w"
    
    type="button" aria-label="Switch branches or tags" tabindex="0" aria-haspopup="true">
    <i>Branch:</i>
    <span class="js-select-button css-truncate-target">master</span>
  </button>

  <div class="select-menu-modal-holder js-menu-content js-navigation-container" data-pjax aria-hidden="true">

    <div class="select-menu-modal">
      <div class="select-menu-header">
        <svg aria-label="Close" class="octicon octicon-x js-menu-close" height="16" role="img" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M7.48 8l3.75 3.75-1.48 1.48L6 9.48l-3.75 3.75-1.48-1.48L4.52 8 .77 4.25l1.48-1.48L6 6.52l3.75-3.75 1.48 1.48z"/></svg>
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
               href="/IBM-Bluemix/docs-staging/blob/264_saucelabs_docs_dra/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="264_saucelabs_docs_dra"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                264_saucelabs_docs_dra
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/21650-docIHSSteps/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="21650-docIHSSteps"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                21650-docIHSSteps
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/21650-updateIHSSteps/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="21650-updateIHSSteps"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                21650-updateIHSSteps
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/62339-sktay-toolchains_beta/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="62339-sktay-toolchains_beta"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                62339-sktay-toolchains_beta
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/148183-MQTT-support/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="148183-MQTT-support"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                148183-MQTT-support
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/148440-update-docs-to-reflect-removal-of-V1-APIs-/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="148440-update-docs-to-reflect-removal-of-V1-APIs-"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                148440-update-docs-to-reflect-removal-of-V1-APIs-
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/212368-addressedViolationInCodeBlockForLiberty/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="212368-addressedViolationInCodeBlockForLiberty"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                212368-addressedViolationInCodeBlockForLiberty
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/213742-removeNewlines/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="213742-removeNewlines"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                213742-removeNewlines
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/218862-RemoveBulletForPsirt/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="218862-RemoveBulletForPsirt"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                218862-RemoveBulletForPsirt
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/218862-latestUpdate-v9/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="218862-latestUpdate-v9"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                218862-latestUpdate-v9
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/229786-create-public-ip-doc/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="229786-create-public-ip-doc"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                229786-create-public-ip-doc
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/ARM-mbed-Extension-%23260-/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="ARM-mbed-Extension-#260-"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                ARM-mbed-Extension-#260-
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Adding-recipes-links-%23499/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Adding-recipes-links-#499"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Adding-recipes-links-#499
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Blockchain-not-Exp-%23486/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Blockchain-not-Exp-#486"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Blockchain-not-Exp-#486
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Caroline-August-work/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Caroline-August-work"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Caroline-August-work
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Caroline-September-work/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Caroline-September-work"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Caroline-September-work
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Caroline-starter-work/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Caroline-starter-work"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Caroline-starter-work
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Certificates_peer/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Certificates_peer"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Certificates_peer
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Create-svg-files-files-%23493/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Create-svg-files-files-#493"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Create-svg-files-files-#493
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Creation-of-IoT-for-Automotive-Getting-Started-docs/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Creation-of-IoT-for-Automotive-Getting-Started-docs"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Creation-of-IoT-for-Automotive-Getting-Started-docs
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Crystal4545-patch-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Crystal4545-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Crystal4545-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Crystal4545-patch-2/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Crystal4545-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Crystal4545-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Crystal4545-patch-3/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Crystal4545-patch-3"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Crystal4545-patch-3
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Crystal4545-patch-4/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Crystal4545-patch-4"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Crystal4545-patch-4
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Crystal4545-patch-5/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Crystal4545-patch-5"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Crystal4545-patch-5
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Crystal4545/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Crystal4545"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Crystal4545
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Deprecate-RTI-%23445/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Deprecate-RTI-#445"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Deprecate-RTI-#445
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Doc-improvements/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Doc-improvements"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Doc-improvements
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Durable-shared-subscriptions/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Durable-shared-subscriptions"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Durable-shared-subscriptions
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Ed-sprint77/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Ed-sprint77"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Ed-sprint77
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Eds-August/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Eds-August"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Eds-August
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/External_icon_Feb2/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="External_icon_Feb2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                External_icon_Feb2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Feb-2017/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Feb-2017"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Feb-2017
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Fix-conrefs%23279/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Fix-conrefs#279"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Fix-conrefs#279
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Guest-account-troubleshoot/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Guest-account-troubleshoot"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Guest-account-troubleshoot
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/HNorlen-docs-pull-1076/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="HNorlen-docs-pull-1076"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                HNorlen-docs-pull-1076
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Historian%23243/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Historian#243"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Historian#243
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/ID-edits-to-Driver-Behaviour-overview-docs/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="ID-edits-to-Driver-Behaviour-overview-docs"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                ID-edits-to-Driver-Behaviour-overview-docs
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/ID-edits-to-Map-insights-docs/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="ID-edits-to-Map-insights-docs"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                ID-edits-to-Map-insights-docs
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/IDS57776-removeADDGIT/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="IDS57776-removeADDGIT"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                IDS57776-removeADDGIT
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/IDS577776_update_images/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="IDS577776_update_images"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                IDS577776_update_images
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/IOT-online-Calculator-%23489/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="IOT-online-Calculator-#489"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                IOT-online-Calculator-#489
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Information-Management-Beta/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Information-Management-Beta"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Information-Management-Beta
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/IoT-Platform-defect-doc-work/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="IoT-Platform-defect-doc-work"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                IoT-Platform-defect-doc-work
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Jan-2017-updates/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Jan-2017-updates"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Jan-2017-updates
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/JaniceHamrickBranch/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="JaniceHamrickBranch"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                JaniceHamrickBranch
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/MQTT-support-%23432/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="MQTT-support-#432"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                MQTT-support-#432
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/MessageHub-connector-%23329-/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="MessageHub-connector-#329-"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                MessageHub-connector-#329-
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/RM-Rodrigo-edit-Feb13/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="RM-Rodrigo-edit-Feb13"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                RM-Rodrigo-edit-Feb13
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/RM-Updates-4/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="RM-Updates-4"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                RM-Updates-4
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/RM-Updates-5/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="RM-Updates-5"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                RM-Updates-5
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/RM-Updates-Jan-2/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="RM-Updates-Jan-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                RM-Updates-Jan-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/RM-updates-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="RM-updates-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                RM-updates-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/RM-updates-2/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="RM-updates-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                RM-updates-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/RM-updates-3/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="RM-updates-3"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                RM-updates-3
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/RM-updates-Jan-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="RM-updates-Jan-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                RM-updates-Jan-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Recipes-links-%23442/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Recipes-links-#442"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Recipes-links-#442
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Sec-bluemix-ed/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Sec-bluemix-ed"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Sec-bluemix-ed
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/UpdateDotnetDoc/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="UpdateDotnetDoc"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                UpdateDotnetDoc
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/Updates-and-edits-to-new-Driver-Behavior-admin-feature/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="Updates-and-edits-to-new-Driver-Behavior-admin-feature"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                Updates-and-edits-to-new-Driver-Behavior-admin-feature
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/WebSocket-def%23910/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="WebSocket-def#910"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                WebSocket-def#910
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/accessibility-fixes/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="accessibility-fixes"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                accessibility-fixes
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/acrolinxChecksRA/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="acrolinxChecksRA"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                acrolinxChecksRA
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/analytics-rule-updates/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="analytics-rule-updates"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                analytics-rule-updates
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/appid-vitaly/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="appid-vitaly"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                appid-vitaly
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/automotive-ID-review/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="automotive-ID-review"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                automotive-ID-review
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/benbakowski-patch-2/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="benbakowski-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                benbakowski-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/bhpratt-patch-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="bhpratt-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                bhpratt-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/bhpratt-patch-2/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="bhpratt-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                bhpratt-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/bhpratt-patch-3/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="bhpratt-patch-3"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                bhpratt-patch-3
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/blockchain-extension-%23476-/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="blockchain-extension-#476-"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                blockchain-extension-#476-
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/blockchain-new-process-%23454/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="blockchain-new-process-#454"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                blockchain-new-process-#454
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/bmx_tech_sales_Networking-team_hiro/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="bmx_tech_sales_Networking-team_hiro"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                bmx_tech_sales_Networking-team_hiro
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/bmx_tech_sales_Networking-team_iwinoto/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="bmx_tech_sales_Networking-team_iwinoto"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                bmx_tech_sales_Networking-team_iwinoto
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/boyang9527-patch-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="boyang9527-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                boyang9527-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/bwentwor-patch-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="bwentwor-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                bwentwor-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/bwentwor-patch-2/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="bwentwor-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                bwentwor-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/certificates_test/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="certificates_test"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                certificates_test
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/cleanup/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="cleanup"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                cleanup
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/container-cli-as-a-bx-plugin/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="container-cli-as-a-bx-plugin"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                container-cli-as-a-bx-plugin
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/copyright-year-updates-2017/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="copyright-year-updates-2017"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                copyright-year-updates-2017
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/custom-cards-%23309/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="custom-cards-#309"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                custom-cards-#309
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/custom-device-mgmt-final/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="custom-device-mgmt-final"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                custom-device-mgmt-final
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/danawilson-patch-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="danawilson-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                danawilson-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/douganv-italics-update1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="douganv-italics-update1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                douganv-italics-update1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/douganv-patterns-updated/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="douganv-patterns-updated"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                douganv-patterns-updated
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/douganv-review-update/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="douganv-review-update"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                douganv-review-update
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/dra_selenium_blog_link/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="dra_selenium_blog_link"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                dra_selenium_blog_link
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/fix_limits_table/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="fix_limits_table"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                fix_limits_table
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/fixFormatting/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="fixFormatting"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                fixFormatting
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/fixMyIssue/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="fixMyIssue"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                fixMyIssue
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/getting-started-12/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="getting-started-12"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                getting-started-12
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/getting-started-15/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="getting-started-15"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                getting-started-15
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/gshgui-patch-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="gshgui-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                gshgui-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/implement_external_icon/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="implement_external_icon"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                implement_external_icon
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/information-management-%23447/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="information-management-#447"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                information-management-#447
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/iot-edge-analytics-addition/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="iot-edge-analytics-addition"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                iot-edge-analytics-addition
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/iot-initial/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="iot-initial"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                iot-initial
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/iot-nav-changes/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="iot-nav-changes"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                iot-nav-changes
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/iot-platform-blockchain-merger/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="iot-platform-blockchain-merger"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                iot-platform-blockchain-merger
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/iot-platform-security-iso/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="iot-platform-security-iso"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                iot-platform-security-iso
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/iot-platform-ts/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="iot-platform-ts"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                iot-platform-ts
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/issue-%23562-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="issue-#562-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                issue-#562-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/issue-%23562-2/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="issue-#562-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                issue-#562-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/issue-%23562-3/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="issue-#562-3"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                issue-#562-3
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/issue-%23562/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="issue-#562"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                issue-#562
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/it8-changes/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="it8-changes"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                it8-changes
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/it9-changes/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="it9-changes"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                it9-changes
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/iwinoto-local-removeCloudant/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="iwinoto-local-removeCloudant"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                iwinoto-local-removeCloudant
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jbetht-patch-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="jbetht-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                jbetht-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jbetht-patch-2/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="jbetht-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                jbetht-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jenschlot-patch-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="jenschlot-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                jenschlot-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jgchan-merge-staging-to-production/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="jgchan-merge-staging-to-production"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                jgchan-merge-staging-to-production
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jsg-access-Sept/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="jsg-access-Sept"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                jsg-access-Sept
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jsg-access-branch/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="jsg-access-branch"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                jsg-access-branch
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jsg-branch/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="jsg-branch"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                jsg-branch
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jsg-can-patch-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="jsg-can-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                jsg-can-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jsinger-changed-date-and-copyright/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="jsinger-changed-date-and-copyright"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                jsinger-changed-date-and-copyright
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jsinger-changed-date-and-copyright2/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="jsinger-changed-date-and-copyright2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                jsinger-changed-date-and-copyright2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jsinger-changed-date-and-copyright3/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="jsinger-changed-date-and-copyright3"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                jsinger-changed-date-and-copyright3
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jsinger-new-appid-files/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="jsinger-new-appid-files"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                jsinger-new-appid-files
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jsinger-removed-cordova/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="jsinger-removed-cordova"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                jsinger-removed-cordova
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jsinger-removed-objC-appid/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="jsinger-removed-objC-appid"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                jsinger-removed-objC-appid
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/jsinger-reworked-appid-topics/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="jsinger-reworked-appid-topics"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                jsinger-reworked-appid-topics
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/kKronstainBrown-patch-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="kKronstainBrown-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                kKronstainBrown-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/kKronstainBrown-patch-2/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="kKronstainBrown-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                kKronstainBrown-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/knlyons_addcli/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="knlyons_addcli"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                knlyons_addcli
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/last-updated-code%23366/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="last-updated-code#366"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                last-updated-code#366
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/last_minute_rules_action_changes/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="last_minute_rules_action_changes"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                last_minute_rules_action_changes
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/lopezdsr-patch-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="lopezdsr-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                lopezdsr-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/lopezdsr-patch-3/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="lopezdsr-patch-3"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                lopezdsr-patch-3
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open selected"
               href="/IBM-Bluemix/docs-staging/blob/master/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="master"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                master
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/mdb-di-envprops/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="mdb-di-envprops"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                mdb-di-envprops
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/mdb-dra-jenkins/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="mdb-dra-jenkins"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                mdb-dra-jenkins
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/mdb-insights-feb/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="mdb-insights-feb"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                mdb-insights-feb
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/mdb-insights-notes/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="mdb-insights-notes"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                mdb-insights-notes
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/mekaufman-patch-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="mekaufman-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                mekaufman-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/mekaufman-patch-2-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="mekaufman-patch-2-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                mekaufman-patch-2-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/mekaufman-patch-2/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="mekaufman-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                mekaufman-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/mekaufman-patch-3/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="mekaufman-patch-3"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                mekaufman-patch-3
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/mekaufman-patch-4/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="mekaufman-patch-4"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                mekaufman-patch-4
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/michellepurcell-API-edit/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="michellepurcell-API-edit"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                michellepurcell-API-edit
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/michellepurcell-ID-edits/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="michellepurcell-ID-edits"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                michellepurcell-ID-edits
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/michellepurcell-accessibility-edits/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="michellepurcell-accessibility-edits"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                michellepurcell-accessibility-edits
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/michellepurcell-defect-fix/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="michellepurcell-defect-fix"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                michellepurcell-defect-fix
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/michellepurcell-doc-defects/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="michellepurcell-doc-defects"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                michellepurcell-doc-defects
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/michellepurcell-edits-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="michellepurcell-edits-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                michellepurcell-edits-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/michellepurcell-edits/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="michellepurcell-edits"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                michellepurcell-edits
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/michellepurcell-final-edits-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="michellepurcell-final-edits-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                michellepurcell-final-edits-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/michellepurcell-final-edits/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="michellepurcell-final-edits"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                michellepurcell-final-edits
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/michellepurcell-gateway-doc-enhancements/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="michellepurcell-gateway-doc-enhancements"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                michellepurcell-gateway-doc-enhancements
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/michellepurcell-patch-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="michellepurcell-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                michellepurcell-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/michellepurcell-patch-2/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="michellepurcell-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                michellepurcell-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/michellepurcell-peer-review/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="michellepurcell-peer-review"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                michellepurcell-peer-review
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/michellepurcell-prep-for-editing-2/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="michellepurcell-prep-for-editing-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                michellepurcell-prep-for-editing-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/michellepurcell-prep-for-publishing/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="michellepurcell-prep-for-publishing"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                michellepurcell-prep-for-publishing
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/michellepurcell-qa-review1-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="michellepurcell-qa-review1-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                michellepurcell-qa-review1-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/michellepurcell-qa-review1-2/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="michellepurcell-qa-review1-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                michellepurcell-qa-review1-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/michellepurcell-qa-review1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="michellepurcell-qa-review1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                michellepurcell-qa-review1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/michellepurcell-sprint-80-81-translation-edits/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="michellepurcell-sprint-80-81-translation-edits"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                michellepurcell-sprint-80-81-translation-edits
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/michellepurcell-tctquery-edits/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="michellepurcell-tctquery-edits"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                michellepurcell-tctquery-edits
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/mpurcell-houskeeping/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="mpurcell-houskeeping"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                mpurcell-houskeeping
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/mpurcell-resolution-for-%23826/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="mpurcell-resolution-for-#826"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                mpurcell-resolution-for-#826
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/natural-language-understanding/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="natural-language-understanding"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                natural-language-understanding
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/node-getting-started/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="node-getting-started"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                node-getting-started
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/os_troubleshootin/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="os_troubleshootin"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                os_troubleshootin
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/pr/481/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="pr/481"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                pr/481
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/pr/661/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="pr/661"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                pr/661
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/pr/903/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="pr/903"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                pr/903
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/pr/1683/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="pr/1683"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                pr/1683
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/premature-cloudant%23415/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="premature-cloudant#415"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                premature-cloudant#415
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/revert-1254-tpm-61386-tech-review/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="revert-1254-tpm-61386-tech-review"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                revert-1254-tpm-61386-tech-review
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/rkung-ibm-patch-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="rkung-ibm-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                rkung-ibm-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/rkung-ibm-patch-2/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="rkung-ibm-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                rkung-ibm-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/rkung-ibm-patch-3/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="rkung-ibm-patch-3"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                rkung-ibm-patch-3
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/rkung-ibm-patch-4/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="rkung-ibm-patch-4"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                rkung-ibm-patch-4
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/rkung-ibm-patch-5/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="rkung-ibm-patch-5"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                rkung-ibm-patch-5
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/rti-accessibility/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="rti-accessibility"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                rti-accessibility
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/rti-migration/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="rti-migration"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                rti-migration
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/saving-volume-data/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="saving-volume-data"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                saving-volume-data
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sec-image-updates/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="sec-image-updates"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                sec-image-updates
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/security-images/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="security-images"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                security-images
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sefuhrer-fix-to-h1-and-date/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="sefuhrer-fix-to-h1-and-date"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                sefuhrer-fix-to-h1-and-date
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sefuhrer-fixed-markdown-link-nested-in-HTML/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="sefuhrer-fixed-markdown-link-nested-in-HTML"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                sefuhrer-fixed-markdown-link-nested-in-HTML
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sefuhrer-fixes-to-h1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="sefuhrer-fixes-to-h1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                sefuhrer-fixes-to-h1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sefuhrer-patch-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="sefuhrer-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                sefuhrer-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sjfink-patch-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="sjfink-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                sjfink-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sjfink-patch-2/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="sjfink-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                sjfink-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sktay-62339-toolchainsbeta/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="sktay-62339-toolchainsbeta"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                sktay-62339-toolchainsbeta
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sktay-patch-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="sktay-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                sktay-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sktay-patch-2/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="sktay-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                sktay-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/sktay/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="sktay"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                sktay
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/smguilia-patch-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="smguilia-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                smguilia-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/smguilia-patch-2/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="smguilia-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                smguilia-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/smguilia-patch-3/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="smguilia-patch-3"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                smguilia-patch-3
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/smoothing-%23472/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="smoothing-#472"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                smoothing-#472
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/stemke-add-resources/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="stemke-add-resources"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                stemke-add-resources
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/stemke-new-folder/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="stemke-new-folder"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                stemke-new-folder
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/stemke-patch-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="stemke-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                stemke-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/stemke-patch-2/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="stemke-patch-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                stemke-patch-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/stemke-patch-3/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="stemke-patch-3"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                stemke-patch-3
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/stemke-patch-4/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="stemke-patch-4"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                stemke-patch-4
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/stemke-patch-5/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="stemke-patch-5"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                stemke-patch-5
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/stemke-patch-6/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="stemke-patch-6"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                stemke-patch-6
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/stemke-patch-7/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="stemke-patch-7"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                stemke-patch-7
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/stemke-patch-8/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="stemke-patch-8"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                stemke-patch-8
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/stemke-patch-9/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="stemke-patch-9"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                stemke-patch-9
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/stemke-patch-10/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="stemke-patch-10"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                stemke-patch-10
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/stemke-patch-11/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="stemke-patch-11"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                stemke-patch-11
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/svkrish-%23405-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="svkrish-#405-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                svkrish-#405-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/svkrish-%23405-2/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="svkrish-#405-2"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                svkrish-#405-2
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/svkrish-%23405-3/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="svkrish-#405-3"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                svkrish-#405-3
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/svkrish-%23405-4/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="svkrish-#405-4"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                svkrish-#405-4
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/svkrish-%23405/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="svkrish-#405"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                svkrish-#405
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/svkrish-patch-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="svkrish-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                svkrish-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/swift-getting-started/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="swift-getting-started"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                swift-getting-started
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/tiona-push-edits/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="tiona-push-edits"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                tiona-push-edits
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/tpm-61353-plans/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="tpm-61353-plans"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                tpm-61353-plans
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/tpm-61386-tech-review/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="tpm-61386-tech-review"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                tpm-61386-tech-review
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/tpm-61485-accessibility/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="tpm-61485-accessibility"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                tpm-61485-accessibility
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/tpm-61570-deprecation-url/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="tpm-61570-deprecation-url"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                tpm-61570-deprecation-url
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/tpm-244037-dedicated-9-30/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="tpm-244037-dedicated-9-30"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                tpm-244037-dedicated-9-30
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/tpm-pipeline-dedicated-beta/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="tpm-pipeline-dedicated-beta"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                tpm-pipeline-dedicated-beta
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/tpm-translation-packaging/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="tpm-translation-packaging"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                tpm-translation-packaging
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/translation_issues/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="translation_issues"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                translation_issues
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/vagrant/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="vagrant"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                vagrant
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/whisk_eventbased/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="whisk_eventbased"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                whisk_eventbased
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/wilburnvanessa-patch-1/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="wilburnvanessa-patch-1"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                wilburnvanessa-patch-1
              </span>
            </a>
            <a class="select-menu-item js-navigation-item js-navigation-open "
               href="/IBM-Bluemix/docs-staging/blob/zOSasaService/services/CloudAutomationManager/cam_managing_connections.md"
               data-name="zOSasaService"
               data-skip-pjax="true"
               rel="nofollow">
              <svg aria-hidden="true" class="octicon octicon-check select-menu-item-icon" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M12 5l-8 8-4-4 1.5-1.5L4 10l6.5-6.5z"/></svg>
              <span class="select-menu-item-text css-truncate-target js-select-menu-filter-text">
                zOSasaService
              </span>
            </a>
        </div>

          <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/IBM-Bluemix/docs-staging/branches" class="js-create-branch select-menu-item select-menu-new-item-form js-navigation-item js-new-item-form" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="c8K5C/nh2juU0AlRLBHhA+/sep1LP7epEUK/vtB7NyCaYKYTOunc6cAHWDLZV+r9j2ba9OMBN+5RhNWlfvVr4w==" /></div>
          <svg aria-hidden="true" class="octicon octicon-git-branch select-menu-item-icon" height="16" version="1.1" viewBox="0 0 10 16" width="10"><path fill-rule="evenodd" d="M10 5c0-1.11-.89-2-2-2a1.993 1.993 0 0 0-1 3.72v.3c-.02.52-.23.98-.63 1.38-.4.4-.86.61-1.38.63-.83.02-1.48.16-2 .45V4.72a1.993 1.993 0 0 0-1-3.72C.88 1 0 1.89 0 3a2 2 0 0 0 1 1.72v6.56c-.59.35-1 .99-1 1.72 0 1.11.89 2 2 2 1.11 0 2-.89 2-2 0-.53-.2-1-.53-1.36.09-.06.48-.41.59-.47.25-.11.56-.17.94-.17 1.05-.05 1.95-.45 2.75-1.25S8.95 7.77 9 6.73h-.02C9.59 6.37 10 5.73 10 5zM2 1.8c.66 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2C1.35 4.2.8 3.65.8 3c0-.65.55-1.2 1.2-1.2zm0 12.41c-.66 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2zm6-8c-.66 0-1.2-.55-1.2-1.2 0-.65.55-1.2 1.2-1.2.65 0 1.2.55 1.2 1.2 0 .65-.55 1.2-1.2 1.2z"/></svg>
            <div class="select-menu-item-text">
              <span class="select-menu-item-heading">Create branch: <span class="js-new-item-name"></span></span>
              <span class="description">from ‘master’</span>
            </div>
            <input type="hidden" name="name" id="name" class="js-new-item-value">
            <input type="hidden" name="branch" id="branch" value="master">
            <input type="hidden" name="path" id="path" value="services/CloudAutomationManager/cam_managing_connections.md">
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

  <div class="BtnGroup float-right">
    <a href="/IBM-Bluemix/docs-staging/find/master"
          class="js-pjax-capture-input btn btn-sm BtnGroup-item"
          data-pjax
          data-hotkey="t">
      Find file
    </a>
    <button aria-label="Copy file path to clipboard" class="js-zeroclipboard btn btn-sm BtnGroup-item tooltipped tooltipped-s" data-copied-hint="Copied!" type="button">Copy path</button>
  </div>
  <div class="breadcrumb js-zeroclipboard-target">
    <span class="repo-root js-repo-root"><span class="js-path-segment"><a href="/IBM-Bluemix/docs-staging"><span>docs-staging</span></a></span></span><span class="separator">/</span><span class="js-path-segment"><a href="/IBM-Bluemix/docs-staging/tree/master/services"><span>services</span></a></span><span class="separator">/</span><span class="js-path-segment"><a href="/IBM-Bluemix/docs-staging/tree/master/services/CloudAutomationManager"><span>CloudAutomationManager</span></a></span><span class="separator">/</span><strong class="final-path">cam_managing_connections.md</strong>
  </div>
</div>


  <div class="commit-tease">
      <span class="float-right">
        <a class="commit-tease-sha" href="/IBM-Bluemix/docs-staging/commit/10541b6d8b1c93934dc907791abc8f2fb94992a7" data-pjax>
          10541b6
        </a>
        <relative-time datetime="2017-02-17T10:02:34Z">Feb 17, 2017</relative-time>
      </span>
      <div>
        <img alt="@gcatasta" class="avatar" height="20" src="https://avatars2.githubusercontent.com/u/20184013?v=3&amp;s=40" width="20" />
        <a href="/gcatasta" class="user-mention" rel="contributor">gcatasta</a>
          <a href="/IBM-Bluemix/docs-staging/commit/10541b6d8b1c93934dc907791abc8f2fb94992a7" class="message" data-pjax="true" title="Update cam_managing_connections.md">Update cam_managing_connections.md</a>
      </div>

    <div class="commit-tease-contributors">
      <button type="button" class="btn-link muted-link contributors-toggle" data-facebox="#blob_contributors_box">
        <strong>1</strong>
         contributor
      </button>
      
    </div>

    <div id="blob_contributors_box" style="display:none">
      <h2 class="facebox-header" data-facebox-id="facebox-header">Users who have contributed to this file</h2>
      <ul class="facebox-user-list" data-facebox-id="facebox-description">
          <li class="facebox-user-list-item">
            <img alt="@gcatasta" height="24" src="https://avatars0.githubusercontent.com/u/20184013?v=3&amp;s=48" width="24" />
            <a href="/gcatasta">gcatasta</a>
          </li>
      </ul>
    </div>
  </div>


<div class="file">
  <div class="file-header">
  <div class="file-actions">

    <div class="BtnGroup">
      <a href="/IBM-Bluemix/docs-staging/raw/master/services/CloudAutomationManager/cam_managing_connections.md" class="btn btn-sm BtnGroup-item" id="raw-url">Raw</a>
        <a href="/IBM-Bluemix/docs-staging/blame/master/services/CloudAutomationManager/cam_managing_connections.md" class="btn btn-sm js-update-url-with-hash BtnGroup-item" data-hotkey="b">Blame</a>
      <a href="/IBM-Bluemix/docs-staging/commits/master/services/CloudAutomationManager/cam_managing_connections.md" class="btn btn-sm BtnGroup-item" rel="nofollow">History</a>
    </div>

        <a class="btn-octicon tooltipped tooltipped-nw"
           href="https://windows.github.com"
           aria-label="Open this file in GitHub Desktop"
           data-ga-click="Repository, open with desktop, type:windows">
            <svg aria-hidden="true" class="octicon octicon-device-desktop" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M15 2H1c-.55 0-1 .45-1 1v9c0 .55.45 1 1 1h5.34c-.25.61-.86 1.39-2.34 2h8c-1.48-.61-2.09-1.39-2.34-2H15c.55 0 1-.45 1-1V3c0-.55-.45-1-1-1zm0 9H1V3h14v8z"/></svg>
        </a>

        <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/IBM-Bluemix/docs-staging/edit/master/services/CloudAutomationManager/cam_managing_connections.md" class="inline-form js-update-url-with-hash" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="HP6tnsxxXRUQzLUdGLt9/6jYSOzEnvwjuCio5nAU7jgDA+vQBfpxc7IOVgPS3qNyBZLst88bTdyP8ExykNFnXA==" /></div>
          <button class="btn-octicon tooltipped tooltipped-nw" type="submit"
            aria-label="Edit this file" data-hotkey="e" data-disable-with>
            <svg aria-hidden="true" class="octicon octicon-pencil" height="16" version="1.1" viewBox="0 0 14 16" width="14"><path fill-rule="evenodd" d="M0 12v3h3l8-8-3-3-8 8zm3 2H1v-2h1v1h1v1zm10.3-9.3L12 6 9 3l1.3-1.3a.996.996 0 0 1 1.41 0l1.59 1.59c.39.39.39 1.02 0 1.41z"/></svg>
          </button>
</form>        <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="/IBM-Bluemix/docs-staging/delete/master/services/CloudAutomationManager/cam_managing_connections.md" class="inline-form" method="post"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /><input name="authenticity_token" type="hidden" value="B6aenuRrQhFZYQ0aN+VWUGxAQwDUZHX+4zrXqrCHCR13TEEo1G+Obqum4RL2hCrEMMiKeN4pEutsnTrBnwaUPA==" /></div>
          <button class="btn-octicon btn-octicon-danger tooltipped tooltipped-nw" type="submit"
            aria-label="Delete this file" data-disable-with>
            <svg aria-hidden="true" class="octicon octicon-trashcan" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M11 2H9c0-.55-.45-1-1-1H5c-.55 0-1 .45-1 1H2c-.55 0-1 .45-1 1v1c0 .55.45 1 1 1v9c0 .55.45 1 1 1h7c.55 0 1-.45 1-1V5c.55 0 1-.45 1-1V3c0-.55-.45-1-1-1zm-1 12H3V5h1v8h1V5h1v8h1V5h1v8h1V5h1v9zm1-10H2V3h9v1z"/></svg>
          </button>
</form>  </div>

  <div class="file-info">
      77 lines (44 sloc)
      <span class="file-info-divider"></span>
    2.91 KB
  </div>
</div>

  
  <div id="readme" class="readme blob instapaper_body">
    <article class="markdown-body entry-content" itemprop="text"><table data-table-type="yaml-metadata">
  <thead>
  <tr>
  <th>copyright</th>

  <th>lastupdated</th>
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
  <td><div>2016, 2017</div></td>
  </tr>
  </tbody>
</table></div></td>

  <td><div>2017-02-17</div></td>
  </tr>
  </tbody>
</table>





<p>{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}</p>



<h1><a id="user-content-managing-connections" class="anchor" href="#managing-connections" aria-hidden="true"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Managing connections</h1>



<p>{: #cam_managing_connections}</p>





<p>In the Connections view, manage your connections to define the parameters to connect to the cloud providers where you want to deploy your templates.
{:shortdesc}</p>

<p>A connection to Bluemix is created by default. If you want to use Bluemix as cloud provider, edit the connection to specify the required parameters.</p>

<p>To add a new connection, follow these steps:</p>

<ol>
<li><p>Click <strong>Clouds</strong>.</p></li>
<li><p>Click <strong>Create Connections</strong>. </p></li>
<li><p>Select the cloud provider to which you want you connect. The supported cloud providers are Amazon EC2 and Bluemix.</p></li>
<li><p>Click <strong>Next</strong>.</p></li>
<li><p>Enter the connection name and description, and specify the required connection parameters depending on the cloud provider you selected.</p></li>
<li><p>Click <strong>Create</strong>. The connection is added to the connection list.</p></li>
</ol>

<p>To edit an existing connection, follow these steps:</p>

<ol>
<li><p>Click <strong>Clouds</strong>.</p></li>
<li><p>In the connection list, click the connection that you want to edit.</p></li>
<li><p>Modify the existing connection details and parameters.</p></li>
<li><p>Click <strong>Update</strong>.</p></li>
</ol>

<p>To delete a connection, follow these steps:</p>

<ol>
<li><p>Click <strong>Clouds</strong>.</p></li>
<li><p>In the connection list, click in the <strong>ACTIONS</strong> column on the right of the connection that you want to delete.</p></li>
<li><p>In the action list, click <strong>Delete Connection</strong>. A confirmation window is opened.</p></li>
<li><p>Click <strong>Delete</strong> to confirm that you want to delete the connection.</p></li>
</ol>
</article>
  </div>

</div>

<button type="button" data-facebox="#jump-to-line" data-facebox-class="linejump" data-hotkey="l" class="d-none">Jump to Line</button>
<div id="jump-to-line" style="display:none">
  <!-- '"` --><!-- </textarea></xmp> --></option></form><form accept-charset="UTF-8" action="" class="js-jump-to-line-form" method="get"><div style="margin:0;padding:0;display:inline"><input name="utf8" type="hidden" value="&#x2713;" /></div>
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
    <ul class="site-footer-links float-right">
        <li><a href="https://github.com/contact" data-ga-click="Footer, go to contact, text:contact">Contact GitHub</a></li>
      <li><a href="https://developer.github.com" data-ga-click="Footer, go to api, text:api">API</a></li>
      <li><a href="https://training.github.com" data-ga-click="Footer, go to training, text:training">Training</a></li>
      <li><a href="https://shop.github.com" data-ga-click="Footer, go to shop, text:shop">Shop</a></li>
        <li><a href="https://github.com/blog" data-ga-click="Footer, go to blog, text:blog">Blog</a></li>
        <li><a href="https://github.com/about" data-ga-click="Footer, go to about, text:about">About</a></li>

    </ul>

    <a href="https://github.com" aria-label="Homepage" class="site-footer-mark" title="GitHub">
      <svg aria-hidden="true" class="octicon octicon-mark-github" height="24" version="1.1" viewBox="0 0 16 16" width="24"><path fill-rule="evenodd" d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0 0 16 8c0-4.42-3.58-8-8-8z"/></svg>
</a>
    <ul class="site-footer-links">
      <li>&copy; 2017 <span title="0.16579s from github-fe146-cp1-prd.iad.github.net">GitHub</span>, Inc.</li>
        <li><a href="https://github.com/site/terms" data-ga-click="Footer, go to terms, text:terms">Terms</a></li>
        <li><a href="https://github.com/site/privacy" data-ga-click="Footer, go to privacy, text:privacy">Privacy</a></li>
        <li><a href="https://github.com/security" data-ga-click="Footer, go to security, text:security">Security</a></li>
        <li><a href="https://status.github.com/" data-ga-click="Footer, go to status, text:status">Status</a></li>
        <li><a href="https://help.github.com" data-ga-click="Footer, go to help, text:help">Help</a></li>
    </ul>
  </div>
</div>



  

  <div id="ajax-error-message" class="ajax-error-message flash flash-error">
    <svg aria-hidden="true" class="octicon octicon-alert" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M8.865 1.52c-.18-.31-.51-.5-.87-.5s-.69.19-.87.5L.275 13.5c-.18.31-.18.69 0 1 .19.31.52.5.87.5h13.7c.36 0 .69-.19.86-.5.17-.31.18-.69.01-1L8.865 1.52zM8.995 13h-2v-2h2v2zm0-3h-2V6h2v4z"/></svg>
    <button type="button" class="flash-close js-flash-close js-ajax-error-dismiss" aria-label="Dismiss error">
      <svg aria-hidden="true" class="octicon octicon-x" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M7.48 8l3.75 3.75-1.48 1.48L6 9.48l-3.75 3.75-1.48-1.48L4.52 8 .77 4.25l1.48-1.48L6 6.52l3.75-3.75 1.48 1.48z"/></svg>
    </button>
    You can't perform that action at this time.
  </div>


    
    <script crossorigin="anonymous" integrity="sha256-UGFpyy/nYlS5IejJRN1AblyrLXGeZX6s6K2phIYjFHI=" src="https://assets-cdn.github.com/assets/frameworks-506169cb2fe76254b921e8c944dd406e5cab2d719e657eace8ada98486231472.js"></script>
    <script async="async" crossorigin="anonymous" integrity="sha256-nrR/vKgzIgtY04IzQr+/baIfC0MMDbvXMn+eNDU7rcU=" src="https://assets-cdn.github.com/assets/github-9eb47fbca833220b58d3823342bfbf6da21f0b430c0dbbd7327f9e34353badc5.js"></script>
    
    
    
    
  <div class="js-stale-session-flash stale-session-flash flash flash-warn flash-banner d-none">
    <svg aria-hidden="true" class="octicon octicon-alert" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M8.865 1.52c-.18-.31-.51-.5-.87-.5s-.69.19-.87.5L.275 13.5c-.18.31-.18.69 0 1 .19.31.52.5.87.5h13.7c.36 0 .69-.19.86-.5.17-.31.18-.69.01-1L8.865 1.52zM8.995 13h-2v-2h2v2zm0-3h-2V6h2v4z"/></svg>
    <span class="signed-in-tab-flash">You signed in with another tab or window. <a href="">Reload</a> to refresh your session.</span>
    <span class="signed-out-tab-flash">You signed out in another tab or window. <a href="">Reload</a> to refresh your session.</span>
  </div>
  <div class="facebox" id="facebox" style="display:none;">
  <div class="facebox-popup">
    <div class="facebox-content" role="dialog" aria-labelledby="facebox-header" aria-describedby="facebox-description">
    </div>
    <button type="button" class="facebox-close js-facebox-close" aria-label="Close modal">
      <svg aria-hidden="true" class="octicon octicon-x" height="16" version="1.1" viewBox="0 0 12 16" width="12"><path fill-rule="evenodd" d="M7.48 8l3.75 3.75-1.48 1.48L6 9.48l-3.75 3.75-1.48-1.48L4.52 8 .77 4.25l1.48-1.48L6 6.52l3.75-3.75 1.48 1.48z"/></svg>
    </button>
  </div>
</div>


  </body>
</html>

