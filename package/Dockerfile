FROM rancher/agent-base:v0.3.0
ENV CNI v0.3.0
ENV RANCHER_CNI_BRIDGE v0.1.3
ENV RANCHER_CNI_IPAM v0.1.1

ADD strongswan.tar.gz /
RUN mkdir -p /opt/cni/bin /etc/cni/net.d && \
    curl -sfSL https://github.com/containernetworking/cni/releases/download/${CNI}/cni-${CNI}.tgz | \
       tar xvzf - -C /tmp ./loopback && \
    curl -sfSL https://github.com/rancher/rancher-cni-bridge/releases/download/${RANCHER_CNI_BRIDGE}/rancher-cni-bridge-${RANCHER_CNI_BRIDGE}.tar.gz | \
    tar xvzf - -C /tmp \
    && mkdir -p /opt/cni/bin \
    && mv /tmp/rancher-cni-bridge /opt/cni/bin/rancher-bridge \
    && mv /tmp/loopback /opt/cni/bin/loopback && \
    curl -sfSL https://github.com/rancher/rancher-cni-ipam/releases/download/${RANCHER_CNI_IPAM}/rancher-cni-ipam-${RANCHER_CNI_IPAM}.tar.gz | \
    tar xvzf - -C /opt/cni/bin

COPY start.sh start-vxlan.sh rancher-net /usr/bin/
CMD ["start.sh"]
