FROM kadalu/kadalu-base

RUN yum install -y glusterfs-fuse
RUN python3 -m pip install grpcio googleapis-common-protos

RUN mkdir -p /kadalu/volfiles /kadalu/templates

COPY lib/kadalulib.py          /kadalu/
COPY csi/controllerserver.py   /kadalu/
COPY csi/csi_pb2_grpc.py       /kadalu/
COPY csi/csi_pb2.py            /kadalu/
COPY csi/identityserver.py     /kadalu/
COPY csi/main.py               /kadalu/
COPY csi/nodeserver.py         /kadalu/
COPY csi/volumeutils.py        /kadalu/
COPY lib/startup.sh            /kadalu/

COPY templates/Replica1.client.vol.j2 /kadalu/templates/
COPY templates/Replica2.client.vol.j2 /kadalu/templates/
COPY templates/Replica3.client.vol.j2 /kadalu/templates/

RUN chmod +x /kadalu/startup.sh

ARG version="(unknown)"
# Container build time (date -u '+%Y-%m-%dT%H:%M:%S.%NZ')
ARG builddate="(unknown)"

LABEL build-date="${builddate}"
LABEL io.k8s.description="KaDalu CSI driver"
LABEL name="kadalu-csi"
LABEL Summary="KaDalu CSI driver"
LABEL vcs-type="git"
LABEL vcs-url="https://github.com/kadalu/kadalu"
LABEL vendor="org.kadalu.gluster"
LABEL version="${version}"

ENTRYPOINT ["/kadalu/startup.sh", "/usr/bin/python3", "/kadalu/main.py"]

# Debugging, Comment the above line and
# uncomment below line
# ENTRYPOINT ["tail", "-f", "/dev/null"]
