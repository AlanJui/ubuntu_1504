建置及佈署使用 MongoDB 的 Web App
=============================

# 建立 MongoDB Server

1. 執行「MongoDB點擊部署方案」

  https://console.developers.google.com/project/_/mc/template/mongodb?_ga=1.59259821.1032602830.1440057453

  Google Developers Console / Project ID / 運算 / Compute Engine

2. 設定 MongoDB Server

  依據下列規格，進行設定。

  * MongoDB Server nodes:
      - Node count: 1
      - Machine type: n1-standard-1
      - Data disk type: 標準永久磁碟
      - Data disk size (GB): 10

  * MongoDB Arbiter nodes:
    - Node count: 0
    - Machine type: f1-micro (1 vCPU, 0.6 GB RAM)

  __設定完成後，須記下 External IP 位址。__

3. 設定防火牆

  ```
  gcloud compute firewall-rules create default-allow-mongo \  
       --allow tcp:27017 \  
       --source-ranges 0.0.0.0/0 \  
       --target-tags mongodb \  
       --description "Allow mongodb access to all IPs"
```

  ```
  alanjui@SRV01:~/workspace/Google-Cloud/myBookShelf001$ gcloud compute firewall-rules create default-allow-mongo \
  >     --allow tcp:27017 \
  >     --source-ranges 0.0.0.0/0 \
  >     --target-tags mongodb \
  >     --description "Allow mongodb access to all IPs"
  Created [https://www.googleapis.com/compute/v1/projects/mybookshelf001/global/firewalls/default-allow-mongo].
  NAME                NETWORK SRC_RANGES RULES     SRC_TAGS TARGET_TAGS
  default-allow-mongo default 0.0.0.0/0  tcp:27017          mongodb
  alanjui@SRV01:~/workspace/Google-Cloud/myBookShelf001$ cd ..
  alanjui@SRV01:~/workspace/Google-Cloud$ git clone https://github.com/GoogleCloudPlatform/nodejs-getting-started.git -b 2-structured-data 2-structured-data
  Cloning into '2-structured-data'...
  remote: Counting objects: 329, done.
  remote: Total 329 (delta 0), reused 0 (delta 0), pack-reused 329
  Receiving objects: 100% (329/329), 67.69 KiB | 0 bytes/s, done.
  Resolving deltas: 100% (197/197), done.
  Checking connectivity... done.
  ```

# 佈署 App

1. 設定 config.js ，完成 Web App 佈署用資訊：

  * projectId
  * dataBackend
  * mongodb

  ```
  module.exports = {
    port: '8080',

    dataBackend: 'mongodb',

    gcloud: {
      projectId: 'mybookshelf001'
    },

    mongodb: {
      url: 'mongodb://104.197.24.201:27017/mydb',
      collection: 'books'
    }
  };
  ```

2. 執行佈署指令

  __gcloud preview app deploy app.yaml --set-default__

  ```
  alanjui@SRV01:~/workspace/Google-Cloud/2-structured-data$ gcloud preview app deploy app.yaml --set-default
  You are about to deploy the following modules:
   - mybookshelf001/default (from [/home/alanjui/workspace/Google-Cloud/2-structured-data/app.yaml])
       Deployed URL: [https://mybookshelf001.appspot.com]

  Do you want to continue (Y/n)?  

  Beginning deployment...
  Verifying that Managed VMs are enabled and ready.
  If this is your first deployment, this may take a while...done.

  Provisioning remote build service.
  Created [https://www.googleapis.com/compute/v1/projects/mybookshelf001/global/firewalls/allow-gae-builder].
  NAME              NETWORK SRC_RANGES RULES    SRC_TAGS TARGET_TAGS
  allow-gae-builder default 0.0.0.0/0  tcp:2376          gae-builder
  Copying certificates for secure access. You may be prompted to create an SSH keypair.
  Warning: Permanently added '104.197.62.31' (ECDSA) to the list of known hosts.
  Building and pushing image for module [default]
  ----------------------------- DOCKER BUILD OUTPUT ------------------------------
  Step 0 : FROM gcr.io/google_appengine/nodejs
  ---> 0efe8a31b9b3
  Step 1 : COPY package.json /app/
  ---> 592be7bec19b
  Removing intermediate container a6fb231d8ea2
  Step 2 : RUN npm install
  ---> Running in 8678258429d1
  > sse4_crc32@4.0.1 install /app/node_modules/gcloud/node_modules/hash-stream-validation/node_modules/sse4_crc32
  > node-gyp rebuild
  make: Entering directory `/app/node_modules/gcloud/node_modules/hash-stream-validation/node_modules/sse4_crc32/build'
  CXX(target) Release/obj.target/sse4_crc32/src/sse4_crc32.o
  SOLINK_MODULE(target) Release/obj.target/sse4_crc32.node
  COPY Release/sse4_crc32.node
  make: Leaving directory `/app/node_modules/gcloud/node_modules/hash-stream-validation/node_modules/sse4_crc32/build'
  > kerberos@0.0.12 install /app/node_modules/mongodb/node_modules/mongodb-core/node_modules/kerberos
  > (node-gyp rebuild 2> builderror.log) || (exit 0)
  make: Entering directory `/app/node_modules/mongodb/node_modules/mongodb-core/node_modules/kerberos/build'
  CXX(target) Release/obj.target/kerberos/lib/kerberos.o
  make: Leaving directory `/app/node_modules/mongodb/node_modules/mongodb-core/node_modules/kerberos/build'
  express@4.13.3 node_modules/express
  ├── escape-html@1.0.2
  ├── merge-descriptors@1.0.0
  ├── array-flatten@1.1.1
  ├── content-type@1.0.1
  ├── cookie@0.1.3
  ├── utils-merge@1.0.0
  ├── cookie-signature@1.0.6
  ├── methods@1.1.1
  ├── fresh@0.3.0
  ├── range-parser@1.0.2
  ├── vary@1.0.1
  ├── path-to-regexp@0.1.7
  ├── etag@1.7.0
  ├── parseurl@1.3.0
  ├── content-disposition@0.5.0
  ├── serve-static@1.10.0
  ├── depd@1.0.1
  ├── on-finished@2.3.0 (ee-first@1.1.1)
  ├── qs@4.0.0
  ├── finalhandler@0.4.0 (unpipe@1.0.0)
  ├── debug@2.2.0 (ms@0.7.1)
  ├── proxy-addr@1.0.8 (forwarded@0.1.0, ipaddr.js@1.0.1)
  ├── send@0.13.0 (destroy@1.0.3, statuses@1.2.1, ms@0.7.1, mime@1.3.4, http-errors@1.3.1)
  ├── type-is@1.6.7 (media-typer@0.3.0, mime-types@2.1.5)
  └── accepts@1.2.12 (negotiator@0.5.3, mime-types@2.1.5)

  body-parser@1.13.3 node_modules/body-parser
  ├── bytes@2.1.0
  ├── content-type@1.0.1
  ├── depd@1.0.1
  ├── qs@4.0.0
  ├── on-finished@2.3.0 (ee-first@1.1.1)
  ├── http-errors@1.3.1 (inherits@2.0.1, statuses@1.2.1)
  ├── raw-body@2.1.2 (unpipe@1.0.0)
  ├── debug@2.2.0 (ms@0.7.1)
  ├── type-is@1.6.7 (media-typer@0.3.0, mime-types@2.1.5)
  └── iconv-lite@0.4.11

  mysql@2.9.0 node_modules/mysql
  ├── readable-stream@1.1.13 (inherits@2.0.1, isarray@0.0.1, string_decoder@0.10.31, core-util-is@1.0.1)
  └── bignumber.js@2.0.7

  prompt@0.2.14 node_modules/prompt
  ├── revalidator@0.1.8
  ├── pkginfo@0.3.0
  ├── read@1.0.7 (mute-stream@0.0.5)
  ├── winston@0.8.3 (cycle@1.0.3, stack-trace@0.0.9, eyes@0.1.8, isstream@0.1.2, colors@0.6.2, async@0.2.10)
  └── utile@0.2.1 (deep-equal@1.0.0, ncp@0.4.2, async@0.2.10, i@0.3.3, mkdirp@0.5.1, rimraf@2.4.3)

  jade@1.11.0 node_modules/jade
  ├── character-parser@1.2.1
  ├── void-elements@2.0.1
  ├── commander@2.6.0
  ├── mkdirp@0.5.1 (minimist@0.0.8)
  ├── jstransformer@0.0.2 (is-promise@2.0.0, promise@6.1.0)
  ├── constantinople@3.0.2 (acorn@2.3.0)
  ├── with@4.0.3 (acorn@1.2.2, acorn-globals@1.0.5)
  ├── clean-css@3.4.0 (commander@2.8.1, source-map@0.4.4)
  ├── uglify-js@2.4.24 (uglify-to-browserify@1.0.2, async@0.2.10, yargs@3.5.4, source-map@0.1.34)
  └── transformers@2.1.0 (promise@2.0.0, css@1.0.8, uglify-js@2.2.5)

  lodash@3.10.1 node_modules/lodash

  gcloud@0.20.0 node_modules/gcloud
  ├── propprop@0.3.0
  ├── prop-assign@1.0.0
  ├── string-format-obj@1.0.1
  ├── arrify@1.0.0
  ├── methmeth@1.1.0
  ├── buffer-equal@0.0.1
  ├── extend@2.0.1
  ├── is@3.0.1
  ├── once@1.3.2 (wrappy@1.0.1)
  ├── dns-zonefile@0.1.9
  ├── node-uuid@1.4.3
  ├── stream-events@1.0.1 (stubs@1.1.2)
  ├── async@0.9.2
  ├── stream-forward@3.0.0 (stubs@2.0.0)
  ├── split-array-stream@1.0.0 (is-stream-ended@0.1.0, async@1.4.2)
  ├── mime-types@2.1.5 (mime-db@1.17.0)
  ├── configstore@1.2.1 (os-tmpdir@1.0.1, object-assign@3.0.0, graceful-fs@4.1.2, uuid@2.0.1, xdg-basedir@2.0.0, osenv@0.1.3, write-file-atomic@1.1.2, mkdirp@0.5.1)
  ├── concat-stream@1.5.0 (inherits@2.0.1, typedarray@0.0.6, readable-stream@2.0.2)
  ├── through2@2.0.0 (xtend@4.0.0, readable-stream@2.0.2)
  ├── duplexify@3.4.2 (end-of-stream@1.0.0, readable-stream@2.0.2)
  ├── retry-request@1.2.1 (stream-cache@0.0.2)
  ├── request@2.61.0 (aws-sign2@0.5.0, stringstream@0.0.4, forever-agent@0.6.1, caseless@0.11.0, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, extend@3.0.0, qs@4.0.0, form-data@1.0.0-rc3, combined-stream@1.0.5, http-signature@0.11.0, bl@1.0.0, tough-cookie@2.0.0, hawk@3.1.0, har-validator@1.8.0)
  ├── google-auto-auth@0.2.1 (object-assign@3.0.0, google-auth-library@0.9.6)
  ├── gce-images@0.1.0 (object-assign@3.0.0, async@1.4.2, got@4.1.1, google-auto-auth@0.1.1)
  ├── protobufjs@3.8.2 (ascli@0.3.0, bytebuffer@3.5.5)
  └── hash-stream-validation@0.1.0 (sse4_crc32@4.0.1)

  mongodb@2.0.42 node_modules/mongodb
  ├── readable-stream@1.0.31 (isarray@0.0.1, inherits@2.0.1, string_decoder@0.10.31, core-util-is@1.0.1)
  ├── es6-promise@2.1.1
  └── mongodb-core@1.2.10 (bson@0.4.11, kerberos@0.0.12)
  ---> 4218e8ebdbd1
  Removing intermediate container 8678258429d1
  Step 3 : COPY . /app/
  ---> 7e117742676b
  Removing intermediate container e2cd528ed040
  Step 4 : CMD npm start
  ---> Running in 3784ab883099
  ---> a34bd8fc8141
  Removing intermediate container 3784ab883099
  Successfully built a34bd8fc8141
  --------------------------------------------------------------------------------

  Updating module [default]...-Deleted [https://www.googleapis.com/compute/v1/projects/mybookshelf001/zones/us-central1-f/instances/gae-builder-vm-20150827t195259].
  Updating module [default]...done.
  Deployed module [default] to [https://mybookshelf001.appspot.com]
  alanjui@SRV01:~/workspace/Google-Cloud/2-structured-data$
  ```
