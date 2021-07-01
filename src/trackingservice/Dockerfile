# Copyright 2020 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.


FROM openjdk:8-jre-slim

#
# Configuration
#

ARG DIVOLTE_VERSION=0.9.0


#
# Install dependencies and Divolte
#

RUN apt-get update && \
    apt-get install -y curl;\
    mkdir -p /opt/divolte && \
    cd /tmp/ && \
    curl -O http://divolte-releases.s3-website-eu-west-1.amazonaws.com/divolte-collector/${DIVOLTE_VERSION}/distributions/divolte-collector-${DIVOLTE_VERSION}.tar.gz && \
    echo "4fa6b3847d3a047a2b5e854aa977012772d552ffa0acf84847042e96c9bb0769  divolte-collector-${DIVOLTE_VERSION}.tar.gz" | sha256sum -c - && \
    tar zxpf divolte-collector-${DIVOLTE_VERSION}.tar.gz -C /opt/divolte && \
    mv /opt/divolte/divolte-collector-${DIVOLTE_VERSION}/ /opt/divolte/divolte-collector && \
    apt-get remove -y  curl && \
    apt-get autoremove -y && \
    apt-get clean -y && \
    rm -fr /var/tmp/* /tmp/*

#
# Configuration changes using divolte-collector.conf
#
COPY conf/ /opt/divolte/divolte-collector/conf/
COPY start.sh /opt/divolte/

#
# Expose the Divolte Collector click simulation web page
#
EXPOSE 8290

ARG PROJECT_ID
ENV PROJECT_ID $PROJECT_ID

CMD ["/opt/divolte/start.sh"]
