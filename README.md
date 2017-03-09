# container-service-gitlab-sample

## Overview
This project shows how a common multi-component application can be deployed
on the Bluemix container service. Each component runs in a separate container
or group of containers.

## Flow

             +-----------+
             |           |
             |    User   |                  +-+
             |           |                  |2|
             +-----+-----+                  +-+
        +-+        |
        |1|        |                  +-------------+
        +-+        |                  |             |
                   |                +->  PostgreSQL |
            +------v-------+        | |             |
            |              |        | +-------------+
            |    Gitlab    +--------+
            |              |        |
            +--------------+        |
                                    |   +-----------+
                                    |   |           |
                                    +--->   Redis   |
                                        |           |
                                        +-----------+

                                             +-+
                                             |3|
                                             +-+


1. User interacts with Gitlab via the web interface or by pushing code to a git
   repo. This container runs the main Ruby on Rails application behind NGINX and
   gitlab-workhorse which is a reverse proxy for large HTTP requests like file
   downloads and git push/pull.

2. Gitlab keeps track of projects, merge requests, groups, etc. in PostgreSQL.

3. Redis acts as a job queue for background tasks.


## Included Components
- Bluemix container service
