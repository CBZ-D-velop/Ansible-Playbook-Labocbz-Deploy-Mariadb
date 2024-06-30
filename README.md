# Ansible playbook: labocbz.deploy_mariadb

![Licence Status](https://img.shields.io/badge/licence-MIT-brightgreen)
![CI Status](https://img.shields.io/badge/CI-success-brightgreen)
![Testing Method](https://img.shields.io/badge/Testing%20Method-Ansible%20Molecule-blueviolet)
![Testing Driver](https://img.shields.io/badge/Testing%20Driver-docker-blueviolet)
![Language Status](https://img.shields.io/badge/language-Ansible-red)
![Compagny](https://img.shields.io/badge/Compagny-Labo--CBZ-blue)
![Author](https://img.shields.io/badge/Author-Lord%20Robin%20Crombez-blue)

## Description

![Tag: Ansible](https://img.shields.io/badge/Tech-Ansible-orange)
![Tag: Debian](https://img.shields.io/badge/Tech-Debian-orange)
![Tag: Mariadb](https://img.shields.io/badge/Tech-Mariadb-orange)
![Tag: SSL/TLS](https://img.shields.io/badge/Tech-SSL%2FTLS-orange)
![Tag: mTLS](https://img.shields.io/badge/Tech-mTLS-orange)
![Tag: MaxScale](https://img.shields.io/badge/Tech-MaxScale-orange)

An Ansible playbook to deploy and configure MariaDB on your host.

This playbook streamlines the installation and configuration of MariaDB. It offers the flexibility to configure a multi-master cluster using Galera. The playbook is adept at setting up and configuring the cluster while also allowing you to modify and customize an administrative account for enhanced security. Additionally, it automates the steps typically carried out by the mysql_secure_installation command, making your MariaDB deployment and management even more convenient and secure.

Furthermore, Apache2 is installed and configured to serve as the HTTP reverse proxy for the MaxScale HTTP Admin Web UI. This component allows for secure access to the MaxScale administration interface, providing encrypted communication channels to safeguard sensitive administrative operations.

This Ansible role can also be extended to incorporate MaxScale, a powerful database proxy that provides advanced database routing, load balancing, and query routing functionalities for MariaDB deployments. Integrating MaxScale into your Ansible playbook enhances the scalability and performance of your MariaDB infrastructure by efficiently distributing database traffic and optimizing query performance. With MaxScale seamlessly integrated into your MariaDB deployment automation, you can achieve unparalleled reliability and efficiency in managing your database clusters.

## Deployment diagramm

![Ansible-Playbook-Labocbz-Deploy-Mariadb](./assets/Ansible-Playbook-Labocbz-Deploy-Mariadb.drawio.svg)

This diagram depicts a potential deployment achieved with the described playbook. At its core lies a MariaDB service component, with three MariaDB instances distributed across three servers. These nodes interact with each other, forming a multi-master cluster, which offers advantages such as high availability and scalability.

To bolster the resilience and performance of this multi-master cluster, MaxScale is integrated as an additional layer in the architecture. MaxScale functions as a database proxy, offering advanced functionalities including database routing, load balancing, and query routing. Through this integration, write operations are optimized by directing them to a single node within the cluster, thus mitigating potential lock and write errors that may arise in a traditional multi-master configuration.

In addition to the database components, Apache2 is installed and configured to serve as the HTTP reverse proxy for the MaxScale HTTP Admin Web UI. This component provides secure access to the MaxScale administration interface, ensuring encrypted communication channels and safeguarding sensitive administrative operations.

With MaxScale orchestrating write operations and Apache2 facilitating secure access to the MaxScale administration interface, the Galera multi-master cluster exhibits increased robustness and efficiency. This integrated solution not only enhances the scalability and performance of the database infrastructure but also simplifies management and maintenance tasks, offering a streamlined and resilient solution for your database requirements. Additionally, communications within the deployment are end-to-end encrypted, and the implementation of mTLS further fortifies security, ensuring data integrity and confidentiality.

## Tests and simulations

### Basics

You have to run multiples tests. *tests with an # are mandatory*

```MARKDOWN
# syntax
# converge
# idempotence
# verify
side_effect
```

Executing theses test in this order is called a "scenario" and Molecule can handle them.

Molecule use Ansible and pre configured playbook to create containers, prepare them, converge (run the playbook) and verify its execution.
You can manage multiples scenario with multiples tests in order to get a 100% code coverage.

This playbook contains a ./tests folder. In this folder you can use the inventory or the tower folder to create a simualtion of a real inventory and a real AWX / Tower job execution.

### Command reminder

```SHELL
# Check your YAML syntax
yamllint -c ./.yamllint .

# Check your Ansible syntax and code security
ansible-lint --config=./.ansible-lint .

# Execute and test your playbook
molecule create
molecule list
molecule converge
molecule verify
molecule destroy

# Execute all previous task in one single command
molecule test
```

## Installation

To install this playbook, just copy/import this playbook or raw file into your fresh playbook repository or call it with the "include_playbook/import_playbook" module.

## Usage

### Vars

```YAML
# From inventory
---
# all vars from to put/from your inventory
# see tests/inventory/group_var for all groups and vars.
```

```YAML
# From AWX / Tower
---

```

## Architectural Decisions Records

Here you can put your change to keep a trace of your work and decisions.

### 2023-10-16: First Init

* First init of this playbook with the bootstrap_playbook playbook by Lord Robin Crombez

### 2023-10-19: Fix and Push

* Playbook can deploy Mariadb in cluster or standalone
* Readme and schema added
* Testing method doesn't use the idempotency, because of CI

### 2023-11-11: Prepare Host and Boolean

* Prepare host role is now called
* You can install or not whit a boolean value

### 2023-12-18: System user and logs

* Added system users
* Added log custom rotation

### 2024-03-05: MaxScale

* You can now install MaxScale as proxy balancer
* You can enable the web UI and protect it with SSL/TLS
* Compatible with Galera

### 2024-03-08: Apache2

* MaxScale is now secur with Apache2

### 2024-05-19: New CI

* Added Markdown lint to the CICD
* Rework all Docker images
* Change CICD vars convention
* New workers
* Removed all automation based on branch

## Authors

* Lord Robin Crombez

## Sources

* [Ansible playbook documentation](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_playbooks.html)
* [Ansible Molecule documentation](https://molecule.readthedocs.io/)
* [labocbz.install_mariadb](https://github.com/CBZ-D-velop/Ansible-Role-Labocbz-Install-Mariadb.git)
