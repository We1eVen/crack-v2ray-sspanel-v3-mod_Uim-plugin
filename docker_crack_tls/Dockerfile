# 基础镜像
FROM phusion/baseimage:master-amd64
# 软件源加速
# COPY sources.list /etc/apt/sources.list
RUN apt update
RUN apt-get install wget curl -y
# 设置时区
ENV TZ=Asia/Shanghai

RUN echo "${TZ}" > /etc/timezone \
    && ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime \
    && apt install -y tzdata \
    && rm -rf /var/lib/apt/lists/*
# 安装v2ray
ARG panelurl
ARG panelkey
ARG nodeid
ARG downwithpanel
ARG speedtestrate
ARG paneltype
ARG usemysql

RUN wget -N --no-check-certificate https://raw.githubusercontent.com/RManLuo/crack-v2ray-sspanel-v3-mod_Uim-plugin/master/install-release.sh &&chmod +x install-release.sh
RUN bash install-release.sh --panelurl ${panelurl} --panelkey ${panelkey} --nodeid ${nodeid} --downwithpanel ${downwithpanel} --speedtestrate ${speedtestrate} --paneltype ${paneltype} --usemysql ${usemysql}

#安装 caddy
ARG nodeurl
ARG mail
ARG fakeurl
ARG v2ray_path
ARG v2ray_port

RUN wget -N --no-check-certificate https://raw.githubusercontent.com/RManLuo/crack-v2ray-sspanel-v3-mod_Uim-plugin/master/install_caddy.sh && chmod +x install_caddy.sh
RUN bash install_caddy.sh ${nodeurl} ${mail} ${fakeurl} ${v2ray_path} ${v2ray_port}

COPY ./start.sh /
RUN chmod 755 /start.sh
CMD /start.sh
