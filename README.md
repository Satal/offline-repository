<!-- omit in toc -->
# Offline CentOS Repository

There are times that it is necessary to have local CentOS repositories that are not connected to the Internet but still need to be able to share the updates. This GitHub repository is designed to provide people with a pattern that they could apply to achieve this.

<!-- TABLE OF CONTENTS -->
## Table of Contents <!-- omit in toc -->

- [About The Project](#about-the-project)
- [Structure](#structure)
  - [Internet facing CentOS Repository](#internet-facing-centos-repository)
  - [Network Diode](#network-diode)
  - [Central Offline CentOS Repository](#central-offline-centos-repository)
  - [Offline CentOS Clients](#offline-centos-clients)
  - [Satellite Repositories](#satellite-repositories)
  - [Satellite Clients](#satellite-clients)
- [Built With](#built-with)
- [Getting Started](#getting-started)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [License](#license)

<!-- ABOUT THE PROJECT -->
## About The Project

There are many reason why an organisation may wish to have environments where there is no Internet access. However, these tend to boil down to having something that the organisation wants to keep safe and removing the Internet connectivity helps reduce the possible attack vectors. This could be organisations such as Microsoft wanting to keep their source code safe or Governments wanting to keep their secrets safe.

Maintaining your environments in an offline environment comes with many issues, this is why I felt it worth creating this repository to provide a pattern for achieving this. While this has been developed on CentOS this is just due to the environment I am working in but the pattern could be applied to other similar update approaches.

![Diagram of structure](images/end-to-end.png "Diagram of structure")

## Structure

Let's first start by understanding the parts of this patterna and the role they play.

<!-- INTERNET FACING CENTOS REPOSITORY -->
### Internet facing CentOS Repository

The Internet facing CentOS Repository will be used for downloading the repository files from the standard repository location. Once these files have been downloaded they can be moved into the offline environment.

We will be downloading all the repository files by using reposync. This will allow us to mirror the contents and therefore avoid the problem of always adding the new files to the existing, which would mean the requires disk space will increase faster.

It would also be possible for us to do this through rsync if we wanted.

<!-- NETWORK DIODE -->
### Network Diode

The network diode provides a mechanism for one way communication. We won't be going into the diode or how the transfer from one system to the other happens as this will be specific to the environment you work in.

<!-- CENTRAL OFFLINE CENTOS REPOSITORY -->
### Central Offline CentOS Repository

The offline CentOS Repository is the main location where all the update files are stored for the offline environment.

<!-- OFFLINE CENTOS CLIENTS -->
### Offline CentOS Clients

There's very little point in having an offline repository if there are no clients that will be using the repository. To do this we will need to update the Yum configuration for these boxes to point to our repository rather than the default online CentOS one.

It would also be possible for us to achieve this by doing some funny business with out local DNS but for this pattern we will just be pointing the user to our offline repository.

<!-- SATELLITE REPOSITORIES -->
### Satellite Repositories

If you have further segregation then it may be necessary for you to provide additional satellite repositories. While this could be done in the same manner as the Internet facing CentOS Repository we are going to take a different approach for this.

<!-- SATELLITE CLIENTS -->
### Satellite Clients

Exactly the same as our Offline CentOS Clients, except that we will be pointing them to the Satellite Repositories. We will need to do the same here as far as configuring the Yum repository location but because we will have different Satellite Repositories, when deploying our config we will need to specify the location correctly for each area.

## Built With

While you can implement this pattern using any approach that you like, I will be using the following technologies.

- [Ansible](https://ansible.com) - For automating the deployment
- [Nginx](https://www.nginx.com) - For the web server where the CentOS repositories are presented to their networks.

<!-- GETTING STARTED -->
## Getting Started

COMING SOON ^_^

<!-- ROADMAP -->
## Roadmap

See the [open issues](https://github.com/Satal/offline-centos-repo/issues) for a list of proposed features (and known issues).

<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to be learn, inspire, and create. Any contributions you make are **greatly appreciated**. My intent by making this available is for others to be able to benefit from it but also provide their input on making this even better.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE` for more information.
