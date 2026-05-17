Title: Understanding the image layers | Docker Docs
Mapped Topic: Containers and images
Source URL: https://docs.docker.com/get-started/docker-concepts/building-images/understanding-image-layers/
Source Type: official_docs
Trust Score: 97
Fetched At: 2026-04-17T07:10:34+00:00
Mapped From CSE.md Section: Part 2: G. DevOps / cloud / infra / observability

# Content

# Understanding the image layers

[Explanation](https://docs.docker.com#explanation)

As you learned in [What is an image?](https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-an-image/), container images are composed of layers. And each of these layers, once created, are immutable. But, what does that actually mean? And how are those layers used to create the filesystem a container can use?

[Image layers](https://docs.docker.com#image-layers)

Each layer in an image contains a set of filesystem changes - additions, deletions, or modifications. Letâs look at a theoretical image:

- The first layer adds basic commands and a package manager, such as apt.
- The second layer installs a Python runtime and pip for dependency management.
- The third layer copies in an applicationâs specific requirements.txt file.
- The fourth layer installs that applicationâs specific dependencies.
- The fifth layer copies in the actual source code of the application.

This example might look like:

This is beneficial because it allows layers to be reused between images. For example, imagine you wanted to create another Python application. Due to layering, you can leverage the same Python base. This will make builds faster and reduce the amount of storage and bandwidth required to distribute the images. The image layering might look similar to the following:

Layers let you extend images of others by reusing their base layers, allowing you to add only the data that your application needs.

[Stacking the layers](https://docs.docker.com#stacking-the-layers)

Layering is made possible by content-addressable storage and union filesystems. While this will get technical, hereâs how it works:

- After each layer is downloaded, it is extracted into its own directory on the host filesystem.
- When you run a container from an image, a union filesystem is created where layers are stacked on top of each other, creating a new and unified view.
- When the container starts, its root directory is set to the location of this unified directory, using
`chroot`

.

When the union filesystem is created, in addition to the image layers, a directory is created specifically for the running container. This allows the container to make filesystem changes while allowing the original image layers to remain untouched. This enables you to run multiple containers from the same underlying image.

[Try it out](https://docs.docker.com#try-it-out)

In this hands-on guide, you will create new image layers manually using the [ docker container commit](https://docs.docker.com/reference/cli/docker/container/commit/) command. Note that youâll rarely create images this way, as youâll normally

[use a Dockerfile](https://docs.docker.com/get-started/docker-concepts/building-images/writing-a-dockerfile/). But, it makes it easier to understand how itâs all working.

[Create a base image](https://docs.docker.com#create-a-base-image)

In this first step, you will create your own base image that you will then use for the following steps.

[Download and install](https://www.docker.com/products/docker-desktop/)Docker Desktop.In a terminal, run the following command to start a new container:

`$ docker run --name=base-container -ti ubuntu`

Once the image has been downloaded and the container has started, you should see a new shell prompt. This is running inside your container. It will look similar to the following (the container ID will vary):

`root@d8c5ca119fcd:/#`

Inside the container, run the following command to install Node.js:

`$ apt update && apt install -y nodejs`

When this command runs, it downloads and installs Node inside the container. In the context of the union filesystem, these filesystem changes occur within the directory unique to this container.

Validate if Node is installed by running the following command:

`$ node -e 'console.log("Hello world!")'`

You should then see a âHello world!â appear in the console.

Now that you have Node installed, youâre ready to save the changes youâve made as a new image layer, from which you can start new containers or build new images. To do so, you will use the

command. Run the following command in a new terminal:`docker container commit`

`$ docker container commit -m "Add node" base-container node-base`

View the layers of your image using the

`docker image history`

command:`$ docker image history node-base`

You will see output similar to the following:

`IMAGE CREATED CREATED BY SIZE COMMENT 9e274734bb25 10 seconds ago /bin/bash 157MB Add node cd1dba651b30 7 days ago /bin/sh -c #(nop) CMD ["/bin/bash"] 0B <missing> 7 days ago /bin/sh -c #(nop) ADD file:6089c6bede9eca8ecâ¦ 110MB <missing> 7 days ago /bin/sh -c #(nop) LABEL org.opencontainers.â¦ 0B <missing> 7 days ago /bin/sh -c #(nop) LABEL org.opencontainers.â¦ 0B <missing> 7 days ago /bin/sh -c #(nop) ARG LAUNCHPAD_BUILD_ARCH 0B <missing> 7 days ago /bin/sh -c #(nop) ARG RELEASE 0B`

Note the âAdd nodeâ comment on the top line. This layer contains the Node.js install you just made.

To prove your image has Node installed, you can start a new container using this new image:

`$ docker run node-base node -e "console.log('Hello again')"`

With that, you should get a âHello againâ output in the terminal, showing Node was installed and working.

Now that youâre done creating your base image, you can remove that container:

`$ docker rm -f base-container`

Base image definitionA base image is a foundation for building other images. It's possible to use any images as a base image. However, some images are intentionally created as building blocks, providing a foundation or starting point for an application.

In this example, you probably wonât deploy this

`node-base`

image, as it doesnât actually do anything yet. But itâs a base you can use for other builds.

[Build an app image](https://docs.docker.com#build-an-app-image)

Now that you have a base image, you can extend that image to build additional images.

Start a new container using the newly created node-base image:

`$ docker run --name=app-container -ti node-base`

Inside of this container, run the following command to create a Node program:

`$ echo 'console.log("Hello from an app")' > app.js`

To run this Node program, you can use the following command and see the message printed on the screen:

`$ node app.js`

In another terminal, run the following command to save this containerâs changes as a new image:

`$ docker container commit -c "CMD node app.js" -m "Add app" app-container sample-app`

This command not only creates a new image named

`sample-app`

, but also adds additional configuration to the image to set the default command when starting a container. In this case, you are setting it to automatically run`node app.js`

.In a terminal outside of the container, run the following command to view the updated layers:

`$ docker image history sample-app`

Youâll then see output that looks like the following. Note the top layer comment has âAdd appâ and the next layer has âAdd nodeâ:

`IMAGE CREATED CREATED BY SIZE COMMENT c1502e2ec875 About a minute ago /bin/bash 33B Add app 5310da79c50a 4 minutes ago /bin/bash 126MB Add node 2b7cc08dcdbb 5 weeks ago /bin/sh -c #(nop) CMD ["/bin/bash"] 0B <missing> 5 weeks ago /bin/sh -c #(nop) ADD file:07cdbabf782942af0â¦ 69.2MB <missing> 5 weeks ago /bin/sh -c #(nop) LABEL org.opencontainers.â¦ 0B <missing> 5 weeks ago /bin/sh -c #(nop) LABEL org.opencontainers.â¦ 0B <missing> 5 weeks ago /bin/sh -c #(nop) ARG LAUNCHPAD_BUILD_ARCH 0B <missing> 5 weeks ago /bin/sh -c #(nop) ARG RELEASE 0B`

Finally, start a new container using the brand new image. Since you specified the default command, you can use the following command:

`$ docker run sample-app`

You should see your greeting appear in the terminal, coming from your Node program.

Now that youâre done with your containers, you can remove them using the following command:

`$ docker rm -f app-container`

[Additional resources](https://docs.docker.com#additional-resources)

If youâd like to dive deeper into the things you learned, check out the following resources:

[Next steps](https://docs.docker.com#next-steps)

As hinted earlier, most image builds donât use `docker container commit`

. Instead, youâll use a Dockerfile which automates these steps for you.

[Writing a Dockerfile](https://docs.docker.com/get-started/docker-concepts/building-images/writing-a-dockerfile/)
