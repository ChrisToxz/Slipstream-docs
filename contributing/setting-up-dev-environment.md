---
description: Below the instruction how to install Slipstream in a Development environment.
---

# Setting up dev environment

**Step 1. Clone the project, or fork it first and clone your fork**

I can add you as collaborator if you really want to stick to this project!

```
git clone https://github.com/ChrisToxz/Slipstream-Core
cd Slipstream-Core
```

**Step 2. Check out to `dev` branch**&#x20;

Of course please create your own feature/fix branch when developing, but just lets the app spin up first! I might change to `master` as development branch, and have a `stable` branch instead.

```
git checkout dev
```

**Step 3. Install PHP packages**

In case you have PHP installed, you can just run `composer install`

If not, please run below command inside the project folder to setup a temporarily container to install the required packages.

```
docker run --rm \
    -u "$(id -u):$(id -g)" \
    -v $(pwd):/var/www/html \
    -w /var/www/html \
    laravelsail/php81-composer:latest \
    composer install --ignore-platform-reqs
```

{% hint style="warning" %}
**In case you still use Docker Compose V1:** use `docker-compose` instead
{% endhint %}

**Step 5. Build the image**

```
docker compose -f docker-compose.yml -f docker-compose.dev.yml build
```

**Step 6. Start up the containers (The app, Database, Soketi(Websockets))**

```
docker compose -f docker-compose.yml -f docker-compose.dev.yml up --force-recreate
```

**Step 7: Install NPM packages**

```
# Locally
npm install
# or in Docker
docker exec Slipstream npm install
```

**Step 8: Run Vite (Assets compiler)**

```
# Locally
npm run dev
# or in Docker
docker exec Slipstream npm run dev
```

**Step 9: Ready to rock!** Visit [http://localhost](http://localhost)

You might want to add below into `data/.env`, this will enabled the app in a local enviroment including showing full error messages. (See `.env.example.dev` as reference)

```
APP_ENV=local
APP_DEBUG=true
```
