1. 如果定义了 MessageConverter 对象，它会被自动关联到 AmqpTemplate 对象上
2. 任何org.springframework.amqp.core.Queue定义为bean的都会自动用于在RabbitMQ实例上声明相应的队列
3. 要重试操作，可以启用重试AmqpTemplate（例如，在代理连接丢失的情况下）：
```
spring.rabbitmq.template.retry.enabled = true
spring.rabbitmq.template.retry.initial-interval = 2s
```
默认情况下禁用重试。您还可以RetryTemplate 通过声明RabbitRetryTemplateCustomizerbean来以编程方式自定义。
4. 当Rabbit基础结构存在时，可以使用@RabbitListener来注释任何bean 以创建侦听器端点。如果RabbitListenerContainerFactory 未定义，SimpleRabbitListenerContainerFactory则会自动配置默认值，您可以使用该spring.rabbitmq.listener.type属性来定制它的的直接容器 。如果 定义了 MessageConverter或MessageRecovererbean，它将自动与默认工厂关联。
5. 从版本4.0开始，客户端默认启用自动恢复。虽然与此功能兼容，但Spring AMQP有自己的恢复机制，通常不需要客户端恢复功能。我们建议禁用amqp-client自动恢复，以避免AutoRecoverConnectionNotCurrentlyOpenException在代理可用但连接尚未恢复时获取实例。从版本1.7.1开始，Spring AMQP禁用它，除非您明确创建自己的RabbitMQ连接工厂并将其提供给CachingConnectionFactory。ConnectionFactory由它创建的RabbitMQ 实例RabbitConnectionFactoryBean也默认禁用该选项。