# Microservices Architecture with JHipster Console

This repository contains a microservices architecture and includes docker-compose configuration for running the services locally and monitoring them with JHipster Console. The tutorial for creating this example is available on [Okta Developer Blog]().

**Prerequisites:**
- [Java 8](https://adoptopenjdk.net/)
- [Docker](https://docs.docker.com/install)
- [Docker Compose](https://docs.docker.com/compose/install)
- [Node.js](https://nodejs.org/en/)


## Getting Started

To install this example, run the following commands:
```bash
git clone https://github.com/indiepopart/jhipster-monitoring.git
cd jhipster-monitoring
```

### Create an Application in Okta

Log in to your Okta Developer account (or [sign up](https://developer.okta.com/signup/) if you don’t have an account).

1. From the **Applications** page, choose **Add Application**.
2. On the Create New Application page, select **Web**.


Configure the following authentication settings for the new Web App:
  - Name: give a name for your application
  - Base URIs: http://localhost:8761, http://localhost:8080
  - Login redirect URIs: http://localhost:8761/login, http://localhost:8080/login
  - Grant Type Allowed: Authorization Code and Refresh Token

Copy the **Client ID** and **Client secret**, and find the **Org URL** at the top right corner in the Okta Dashboard.


### Run with Docker Compose

Go to the docker-compose folder in the project and create an **.env** file with the following content:

```
OIDC_CLIENT_ID=<client_id>
OIDC_CLIENT_SECRET=<client_secret>
RESOURCE_USER_INFO_URI=<org_url>/oauth2/default/v1/userinfo
ACCESS_TOKEN_URI=<org_url>/oauth2/default/v1/token
USER_AUTHORIZATION_URI=<org_url>/oauth2/default/v1/authorize
```

Build the services docker images for blog, store and gateway with the following command:

```SHELL
./mvnw package -Pprod -Pzipkin verify jib:dockerBuild -DskipTests
```

Once all the services are built, run docker-compose:
```SHELL
docker-compose up
```

Login to the JHipster Registry at [**http://localhost:8761**](http://localhost:8761) with Okta user credentials and check the service's health.
Then, access the **JHipster Console** at [**http://localhost:5601**](http://localhost:5601).

## Links

[JHipster Monitoring Documentation](https://www.jhipster.tech/monitoring/)

## Help

Please post any questions as comments on the [blog post](), or on the [Okta Developer Forums](https://devforum.okta.com/).

## License

Apache 2.0, see [LICENSE](LICENSE).
