# This file is part of IVRE.
# Copyright 2011 - 2023 Pierre LALET <pierre@droids-corp.org>
#
# IVRE is free software: you can redistribute it and/or modify it
# under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# IVRE is distributed in the hope that it will be useful, but WITHOUT
# ANY WARRANTY; without even the implied warranty of MERCHANTABILITY
# or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public
# License for more details.
#
# You should have received a copy of the GNU General Public License
# along with IVRE. If not, see <http://www.gnu.org/licenses/>.

FROM python:3.13-slim-bookworm
LABEL maintainer="Hostmasters <hostmasters@virus.org>"

ENV DEBIAN_FRONTEND noninteractive

# Install pip, get IVRE, uninstall pip
RUN apt-get -q update && \
    apt-get -qy --no-install-recommends install git libpq-dev ca-certificates && \
    pip install 'setuptools<80.0.0' && \
    pip install git+https://github.com/mort666/ivre && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Fix version
RUN sed -ri 's#$#-docker#' /usr/local/lib/python*/dist-packages/ivre/VERSION && \
    sed -ri 's#(VERSION = .*)(['\''"])$#\1-docker\2#' /usr/local/lib/python*/dist-packages/ivre/__init__.py

RUN echo 'DB = "mongodb://ivredb/"' > /etc/ivre.conf
