# 在官方镜像基础上，启用了一个官方的延迟消息队列插件

FROM rabbitmq:3.8.2-management

COPY ./plugins/rabbitmq_delayed_message_exchange-3.8.0.ez /plugins/

RUN rabbitmq-plugins enable --offline rabbitmq_delayed_message_exchange
