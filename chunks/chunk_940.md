### Post 414
**Post URL**: /t/project-1-llm-based-automation-agent-discussion-thread-tds-jan-2025/164277/414
- **ID**: 595429
- **Author**: Andrew David (23f1002382)
- **Created At**: 2025-02-15T13:57:58.100Z
- **Content**:  
  <aside class="onebox githubfolder" data-onebox-src="https://github.com/ANdIeCOOl/TDS-Project-1/tree/main">
  <header class="source">
      <img src="https://github.githubassets.com/favicons/favicon.svg" class="site-icon" width="32" height="32">

      <a href="https://github.com/ANdIeCOOl/TDS-Project-1/tree/main" target="_blank" rel="noopener nofollow ugc">github.com</a>
  </header>

  <article class="onebox-body">
    <h3><a href="https://github.com/ANdIeCOOl/TDS-Project-1/tree/main" target="_blank" rel="noopener nofollow ugc">GitHub - ANdIeCOOl/TDS-Project-1</a></h3>

  <a href="https://github.com/ANdIeCOOl/TDS-Project-1/tree/main" target="_blank" rel="noopener nofollow ugc">main</a>

  <span class="label1">Contribute to ANdIeCOOl/TDS-Project-1 development by creating an account on GitHub.</span>

  </article>

  <div class="onebox-metadata">
    
    
  </div>

  <div style="clear: both"></div>
</aside>

ATLEAST 6 minimum score use at own risk(MIT LICENCE xD)<br>
<br><br>
BUILD TIME TAKES 2 mins<br>
WITH DOCKER FILE
<pre data-code-wrap="bash"><code class="lang-bash">@ANdIeCOOl ➜ /workspaces/TDS-Project-1/tds-project-1 (main) $ docker build -t tds-project-1 .
[+] Building 123.9s (13/13) FINISHED                                                                       docker:default
 =&gt; [internal] load build definition from Dockerfile                                                                 0.0s
 =&gt; =&gt; transferring dockerfile: 1.18kB                                                                               0.0s
 =&gt; [internal] load metadata for docker.io/library/python:3.11-slim                                                  2.2s
 =&gt; [auth] library/python:pull token for registry-1.docker.io                                                        0.0s
 =&gt; [internal] load .dockerignore                                                                                    0.0s
 =&gt; =&gt; transferring context: 2B                                                                                      0.0s
 =&gt; [internal] load build context                                                                                    0.1s
 =&gt; =&gt; transferring context: 34.30kB                                                                                 0.0s
 =&gt; [1/7] FROM docker.io/library/python:3.11-slim@sha256:42420f737ba91d509fc60d5ed65ed0492678a90c561e1fa08786ae8ba8  8.7s
 =&gt; =&gt; resolve docker.io/library/python:3.11-slim@sha256:42420f737ba91d509fc60d5ed65ed0492678a90c561e1fa08786ae8ba8  0.0s
 =&gt; =&gt; sha256:2c2c44fb54acb184dbedee948d7ba6460b1075a60a014d66857ce46543d4d840 5.29kB / 5.29kB                       0.0s
 =&gt; =&gt; sha256:c29f5b76f736a8b555fd191c48d6581bb918bcd605a7cbcc76205dd6acff3260 28.21MB / 28.21MB                     0.7s
 =&gt; =&gt; sha256:73c4bbda278d9a2b5133d6dabfac3eec43a92b8c8c15da914f298b4c966bea53 3.51MB / 3.51MB                       0.9s
 =&gt; =&gt; sha256:acc53c3e87ac87c98e44b79e0d2a6293146650f5cba576f424dab77f8c0a4335 16.20MB / 16.20MB                     1.6s
 =&gt; =&gt; sha256:42420f737ba91d509fc60d5ed65ed0492678a90c561e1fa08786ae8ba8b52eda 9.13kB / 9.13kB                       0.0s
 =&gt; =&gt; sha256:a66bd09b8d35bb52cd106a94c23a94ba22e6fde6bd13d6c5912ec4f5888a7f14 1.75kB / 1.75kB                       0.0s
 =&gt; =&gt; extracting sha256:c29f5b76f736a8b555fd191c48d6581bb918bcd605a7cbcc76205dd6acff3260                            2.2s
 =&gt; =&gt; sha256:ad3b14759e4f8c9a73d51c897a8b96f022ec96ffc237502ad3f1f12b0b0e361f 249B / 249B                           1.9s
 =&gt; =&gt; extracting sha256:73c4bbda278d9a2b5133d6dabfac3eec43a92b8c8c15da914f298b4c966bea53                            0.2s
 =&gt; =&gt; extracting sha256:acc53c3e87ac87c98e44b79e0d2a6293146650f5cba576f424dab77f8c0a4335                            1.4s
 =&gt; =&gt; extracting sha256:ad3b14759e4f8c9a73d51c897a8b96f022ec96ffc237502ad3f1f12b0b0e361f                            0.0s
 =&gt; [2/7] WORKDIR /app                                                                                               0.2s
 =&gt; [3/7] RUN pip install --upgrade pip setuptools wheel                                                             8.7s
 =&gt; [4/7] RUN apt-get update &amp;&amp; apt-get install -y --no-install-recommends     gcc     g++     make     libffi-dev  84.5s
 =&gt; [5/7] RUN npm install -g prettier                                                                                1.5s
 =&gt; [6/7] COPY app /app                                                                                              0.1s
 =&gt; [7/7] RUN pip install uv                                                                                         4.5s
 =&gt; exporting to image                                                                                              13.4s
 =&gt; =&gt; exporting layers                                                                                             13.4s
 =&gt; =&gt; writing image sha256:39add91710bc7970d44dae04b3f4a0c4f227d1471fac4df7b01cec86ce7af3cf                         0.0s
 =&gt; =&gt; naming to docker.io/library/tds-project-1                                                                     0.0s
</code></pre>
<span class="mention">@ANdIeCOOl</span> ➜ /workspaces/TDS-Project-1/tds-project-1 (main) $ docker images<br>
REPOSITORY      TAG       IMAGE ID       CREATED          SIZE<br>
tds-project-1   latest    39add91710bc   31 seconds ago   923MB
if this cause any issues please notify  <a class="mention" href="/u/s.anand">@s.anand</a>  <a class="mention" href="/u/carlton">@carlton</a> <a class="mention" href="/u/jivraj">@Jivraj</a>
- **Reactions**: None
- **Post Number**: 414

