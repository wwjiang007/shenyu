# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM centos:7 AS prepare

ARG APP_NAME

ENV LOCAL_PATH /opt/shenyu-bootstrap

ADD target/${APP_NAME}.tar.gz /opt
RUN mv /opt/${APP_NAME} ${LOCAL_PATH}

# FROM amazoncorretto:17.0.11-alpine3.19
FROM eclipse-temurin:17-centos7

# RUN apk --no-cache add wget curl

ENV LOCAL_PATH /opt/shenyu-bootstrap
ENV BOOT_JVM ""

COPY --from=prepare ${LOCAL_PATH} ${LOCAL_PATH}
COPY docker/logback.xml ${LOCAL_PATH}/conf/logback.xml
COPY docker/entrypoint.sh ${LOCAL_PATH}/entrypoint.sh
RUN chmod +x ${LOCAL_PATH}/entrypoint.sh

WORKDIR ${LOCAL_PATH}

EXPOSE 9195

ENTRYPOINT ["/bin/sh", "entrypoint.sh"]
