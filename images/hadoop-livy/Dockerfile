ARG VERSION=latest

FROM jcrist/hadoop-testing:$VERSION
LABEL maintainer="jcrist"

# Download and install livy
RUN cd /etc && \
    curl -O http://apache.spinellicreations.com/incubator/livy/0.6.0-incubating/apache-livy-0.6.0-incubating-bin.zip && \
    unzip apache-livy-0.6.0-incubating-bin.zip -d livy && \
    rm apache-livy-0.6.0-incubating-bin.zip

# Create livy keytabs
RUN kadmin.local -q "addprinc -randkey livy/edge.example.com@EXAMPLE.COM" && \
    kadmin.local -q "xst -norandkey -k /etc/livy/livy.keytab livy/edge.example.com HTTP/edge.example.com"

# Copy in livy configuration
COPY livy.conf /etc/livy/conf/livy.conf