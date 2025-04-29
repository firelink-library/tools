---
title: Nós e Tópicos
sidebar_position: 3
slug: /topics
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';
import Admonition from '@theme/Admonition';

# Introdução ao ROS

O ROS nada mais é do que um sistema capaz de provisionar a comunicação entre
nós dentro de uma rede (tipicamente em uma rede local, mas é possível
configurá-lo para acesso através da internet). O seu motivo de existir é para
que seja possível promover uma arquitetura **desacoplada** para códigos de
aplicações de robótica. Essa decisão arquitetural faz com que seja possível o
compartilhamento de algoritmos de difícil implementação de uma forma que seja
fácil integrá-los a qualquer projeto sem nem ao menos entender profundamente
como se dá seu funcionamento. 

Quer um exemplo? Pesquise sobre **filtros de kalmann** ou **slam**. Esses
algoritmos estão sob seu alcance ao utilizar o ROS e seriam bastante onerosos
para implementar do zero.

As únidades fundamentais do ROS são os **nós** e os **tópicos**. A seguir,
vamos ver um pouco melhor como eles funcionam.

## 1. Nós 

<img 
  src="https://docs.ros.org/en/humble/_images/Nodes-TopicandService.gif"
  alt="ROS nodes" 
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '70vh',
    marginRight: 'auto'
  }} 
/>
<br/>

Um "nó" é um dos principais elementos do ROS 2. Cada nó deve ser responsável por
uma única função modular. Por exemplo, um nó pode ser responsável por controlar
os motores das rodas ou por publicar dados de sensores, como um laser
range-finder. Os nós podem enviar e receber dados de outros nós através de
tópicos, serviços, ações ou parâmetros. Um sistema robótico completo é composto
por muitos nós trabalhando em conjunto. Em ROS 2, um único executável (programa
C++, programa Python, etc.) pode conter um ou mais nós.

### 1.1. Interagindo com Nós
Existem várias ferramentas que permitem interagir com os nós em ROS 2:

1. **ros2 run**: Este comando lança um executável de um pacote. Por exemplo,
para executar o "turtlesim", você usaria o comando `ros2 run turtlesim
turtlesim_node`.

2. **ros2 node list**: Este comando mostra os nomes de todos os nós em execução.
É útil quando você quer interagir com um nó ou quando tem muitos nós em execução
e precisa
monitorá-los.

3. **ros2 node info**: Depois de conhecer os nomes dos nós, você pode obter mais
informações sobre eles usando este comando. Ele retorna uma lista de assinantes,
publicadores, serviços e ações, ou seja, as conexões do gráfico ROS que
interagem com aquele
nó.

### 1.2. Remapeamento (Remapping)

O remapeamento permite reatribuir propriedades padrão do nó, como nomes de nós,
nomes de tópicos, nomes de serviços, etc., para valores personalizados. Por
exemplo, você pode reatribuir o nome do nó "/turtlesim" para "/my_turtle" usando
o comando `ros2 run turtlesim turtlesim_node --ros-args --remap
__node:=my_turtle`.

## 2. Tópicos

<img 
  src="https://docs.ros.org/en/humble/_images/Topic-MultiplePublisherandMultipleSubscriber.gif"
  alt="ROS nodes" 
  style={{ 
    display: 'block',
    marginLeft: 'auto',
    maxHeight: '70vh',
    marginRight: 'auto'
  }} 
/>
<br/>

O ROS 2 utiliza tópicos como um dos principais meios de comunicação entre nós. 
Os tópicos permitem que os dados sejam transmitidos entre nós, possibilitando a 
interação e a execução de tarefas complexas em sistemas robóticos. Aqui está um 
guia sobre como os tópicos funcionam no ROS 2, com base no tutorial fornecido.

### 2.1. Configuração Inicial
Antes de começar a explorar os tópicos, você precisa ter o ROS 2 e o pacote turtlesim instalados. Você deve iniciar os nós do turtlesim e do turtle_teleop_key em terminais separados usando os comandos:
```bash
ros2 run turtlesim turtlesim_node
ros2 run turtlesim turtle_teleop_key
```

### 2.2. Visualizando com rqt_graph
O `rqt_graph` é uma ferramenta gráfica que permite visualizar os nós, tópicos e as conexões entre eles. Para executá-lo, use o comando:
```bash
rqt_graph
```
Você verá os nós e tópicos em execução, bem como as conexões entre eles.

### 2.3. Listando Tópicos
Para listar todos os tópicos ativos no sistema, use o comando:
```bash
ros2 topic list
```
Para ver os tipos de mensagens associados a cada tópico, adicione a opção `-t`:
```bash
ros2 topic list -t
```

### 2.4. Visualizando Dados de um Tópico
Para ver os dados sendo publicados em um tópico específico, use o comando:
```bash
ros2 topic echo <nome_do_tópico>
```
Por exemplo:
```bash
ros2 topic echo /turtle1/cmd_vel
```
Isso mostrará os dados sendo publicados no tópico `/turtle1/cmd_vel`.

### 2.5. Informações sobre um Tópico
Para obter informações sobre um tópico específico, como o número de publicadores e assinantes, use o comando:
```bash
ros2 topic info <nome_do_tópico>
```

### 2.6. Visualizando a Estrutura de uma Mensagem
Para ver a estrutura de uma mensagem de um tipo específico, use o comando:
```bash
ros2 interface show <tipo_da_mensagem>
```
Por exemplo:
```bash
ros2 interface show geometry_msgs/msg/Twist
```

### 2.7. Publicando em um Tópico
Você pode publicar dados em um tópico diretamente da linha de comando usando o comando:
```bash
ros2 topic pub <nome_do_tópico> <tipo_da_mensagem> '<dados>'
```
Por exemplo:
```bash
ros2 topic pub /turtle1/cmd_vel geometry_msgs/msg/Twist '{linear: {x: 2.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 1.8}}'
```

### 2.8. Verificando a Taxa de Publicação
Para ver a taxa na qual os dados estão sendo publicados em um tópico, use o comando:
```bash
ros2 topic hz <nome_do_tópico>
```

## 3. Exemplos 

### 3.1. Criando um subscriber simples 

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/7CkcfUkLMWQ" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>

#### 3.1.1. Versão mínima

<Tabs
  defaultValue="rclpy"
  values={[
    {label: 'Python', value: 'rclpy'},
    {label: 'Python c/ lambda', value: 'rclpy-lambda'},
    {label: 'C++ (não recomendado)', value: 'rclcpp'},
  ]}>

<TabItem value="rclpy">

```python showLineNumbers title="Python oldschool"
import rclpy

from std_msgs.msg import String

g_node = None


def chatter_callback(msg):
    global g_node
    g_node.get_logger().info(
        'I heard: "%s"' % msg.data)


def main(args=None):
    global g_node
    rclpy.init(args=args)

    g_node = rclpy.create_node('minimal_subscriber')

    subscription = g_node.create_subscription(String, 'topic', chatter_callback, 10)
    subscription  # prevent unused variable warning

    while rclpy.ok():
        rclpy.spin_once(g_node)

    # Destroy the node explicitly
    # (optional - otherwise it will be done automatically
    # when the garbage collector destroys the node object)
    g_node.destroy_node()
    rclpy.shutdown()


if __name__ == '__main__':
    main()
```

</TabItem>

<TabItem value="rclpy-lambda">

```python showLineNumbers title="Python c/ lambda"
import rclpy

from std_msgs.msg import String


def main(args=None):
    rclpy.init(args=args)

    node = rclpy.create_node('minimal_subscriber')

    subscription = node.create_subscription(
        String, 'topic', lambda msg: node.get_logger().info('I heard: "%s"' % msg.data), 10)
    subscription  # prevent unused variable warning

    rclpy.spin(node)

    # Destroy the node explicitly
    # (optional - otherwise it will be done automatically
    # when the garbage collector destroys the node object)
    node.destroy_node()
    rclpy.shutdown()


if __name__ == '__main__':
    main()
```

</TabItem>

<TabItem value="rclcpp">

```cpp showLineNumbers title="C++"
#include "rclcpp/rclcpp.hpp"
#include "std_msgs/msg/string.hpp"

rclcpp::Node::SharedPtr g_node = nullptr;

/* We do not recommend this style anymore, because composition of multiple
 * nodes in the same executable is not possible. Please see one of the subclass
 * examples for the "new" recommended styles. This example is only included
 * for completeness because it is similar to "classic" standalone ROS nodes. */

void topic_callback(const std_msgs::msg::String & msg)
{
  RCLCPP_INFO(g_node->get_logger(), "I heard: '%s'", msg.data.c_str());
}

int main(int argc, char * argv[])
{
  rclcpp::init(argc, argv);
  g_node = rclcpp::Node::make_shared("minimal_subscriber");
  auto subscription =
    g_node->create_subscription<std_msgs::msg::String>("topic", 10, topic_callback);
  rclcpp::spin(g_node);
  rclcpp::shutdown();
  return 0;
}
```

</TabItem>

</Tabs>

#### 3.1.2. Utilizando orientação à objetos

<Tabs
  defaultValue="rclpy"
  values={[
    {label: 'Python', value: 'rclpy'},
    {label: 'C++', value: 'rclcpp'},
  ]}>

<TabItem value="rclpy">

```python showLineNumbers title="Python OOP"
import rclpy
from rclpy.node import Node

from std_msgs.msg import String


class MinimalSubscriber(Node):

    def __init__(self):
        super().__init__('minimal_subscriber')
        self.subscription = self.create_subscription(
            String,
            'topic',
            self.listener_callback,
            10)
        self.subscription  # prevent unused variable warning

    def listener_callback(self, msg):
        self.get_logger().info('I heard: "%s"' % msg.data)


def main(args=None):
    rclpy.init(args=args)

    minimal_subscriber = MinimalSubscriber()

    rclpy.spin(minimal_subscriber)

    # Destroy the node explicitly
    # (optional - otherwise it will be done automatically
    # when the garbage collector destroys the node object)
    minimal_subscriber.destroy_node()
    rclpy.shutdown()


if __name__ == '__main__':
    main()
```

</TabItem>

<TabItem value="rclcpp">

```cpp showLineNumbers title="C++"
#include <functional>
#include <memory>

#include "rclcpp/rclcpp.hpp"
#include "std_msgs/msg/string.hpp"

using std::placeholders::_1;

class MinimalSubscriber : public rclcpp::Node
{
public:
  MinimalSubscriber()
  : Node("minimal_subscriber")
  {
    subscription_ = this->create_subscription<std_msgs::msg::String>(
      "topic", 10, std::bind(&MinimalSubscriber::topic_callback, this, _1));
  }

private:
  void topic_callback(const std_msgs::msg::String & msg) const
  {
    RCLCPP_INFO(this->get_logger(), "I heard: '%s'", msg.data.c_str());
  }
  rclcpp::Subscription<std_msgs::msg::String>::SharedPtr subscription_;
};

int main(int argc, char * argv[])
{
  rclcpp::init(argc, argv);
  rclcpp::spin(std::make_shared<MinimalSubscriber>());
  rclcpp::shutdown();
  return 0;
}
```
</TabItem>
</Tabs>

### 3.2. Criando um publisher simples

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/R1ulM5XFQ0I" 
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>

#### 3.2.1. Versão mínima

<Tabs
  defaultValue="rclpy"
  values={[
    {label: 'Python', value: 'rclpy'},
    {label: 'C++ (não recomendado)', value: 'rclcpp'},
  ]}>

<TabItem value="rclpy">

```python showLineNumbers title="Python local function"
import rclpy

from std_msgs.msg import String


def main(args=None):
    rclpy.init(args=args)

    node = rclpy.create_node('minimal_publisher')
    publisher = node.create_publisher(String, 'topic', 10)

    msg = String()
    i = 0

    def timer_callback():
        nonlocal i
        msg.data = 'Hello World: %d' % i
        i += 1
        node.get_logger().info('Publishing: "%s"' % msg.data)
        publisher.publish(msg)

    timer_period = 0.5  # seconds
    timer = node.create_timer(timer_period, timer_callback)

    rclpy.spin(node)

    # Destroy the timer attached to the node explicitly
    # (optional - otherwise it will be done automatically
    # when the garbage collector destroys the node object)
    node.destroy_timer(timer)
    node.destroy_node()
    rclpy.shutdown()


if __name__ == '__main__':
    main()
```

</TabItem>

<TabItem value="rclcpp">

```cpp showLineNumbers title="C++ (não recomendado)"
#include <chrono>
#include <string>

#include "rclcpp/rclcpp.hpp"
#include "std_msgs/msg/string.hpp"

using namespace std::chrono_literals;

/* We do not recommend this style anymore, because composition of multiple
 * nodes in the same executable is not possible. Please see one of the subclass
 * examples for the "new" recommended styles. This example is only included
 * for completeness because it is similar to "classic" standalone ROS nodes. */

int main(int argc, char * argv[])
{
  rclcpp::init(argc, argv);
  auto node = rclcpp::Node::make_shared("minimal_publisher");
  auto publisher = node->create_publisher<std_msgs::msg::String>("topic", 10);
  std_msgs::msg::String message;
  auto publish_count = 0;
  rclcpp::WallRate loop_rate(500ms);

  while (rclcpp::ok()) {
    message.data = "Hello, world! " + std::to_string(publish_count++);
    RCLCPP_INFO(node->get_logger(), "Publishing: '%s'", message.data.c_str());
    try {
      publisher->publish(message);
      rclcpp::spin_some(node);
    } catch (const rclcpp::exceptions::RCLError & e) {
      RCLCPP_ERROR(
        node->get_logger(),
        "unexpectedly failed with %s",
        e.what());
    }
    loop_rate.sleep();
  }
  rclcpp::shutdown();
  return 0;
}
```
</TabItem>
</Tabs>

#### 3.2.2. Utilizando orientação à objetos

<Tabs
  defaultValue="rclpy"
  values={[
    {label: 'Python', value: 'rclpy'},
    {label: 'C++', value: 'rclcpp'},
  ]}>

<TabItem value="rclpy">

```python showLineNumbers title="Python OOP"
import rclpy
from rclpy.node import Node

from std_msgs.msg import String


class MinimalPublisher(Node):

    def __init__(self):
        super().__init__('minimal_publisher')
        self.publisher_ = self.create_publisher(String, 'topic', 10)
        timer_period = 0.5  # seconds
        self.timer = self.create_timer(timer_period, self.timer_callback)
        self.i = 0

    def timer_callback(self):
        msg = String()
        msg.data = 'Hello World: %d' % self.i
        self.publisher_.publish(msg)
        self.get_logger().info('Publishing: "%s"' % msg.data)
        self.i += 1


def main(args=None):
    rclpy.init(args=args)

    minimal_publisher = MinimalPublisher()

    rclpy.spin(minimal_publisher)

    # Destroy the node explicitly
    # (optional - otherwise it will be done automatically
    # when the garbage collector destroys the node object)
    minimal_publisher.destroy_node()
    rclpy.shutdown()


if __name__ == '__main__':
    main()
```

</TabItem>

<TabItem value="rclcpp">

```cpp showLineNumbers title="C++"
#include <chrono>
#include <functional>
#include <memory>
#include <string>

#include "rclcpp/rclcpp.hpp"
#include "std_msgs/msg/string.hpp"

using namespace std::chrono_literals;

/* This example creates a subclass of Node and uses std::bind() to register a
 * member function as a callback from the timer. */

class MinimalPublisher : public rclcpp::Node
{
public:
  MinimalPublisher()
  : Node("minimal_publisher"), count_(0)
  {
    publisher_ = this->create_publisher<std_msgs::msg::String>("topic", 10);
    timer_ = this->create_wall_timer(
      500ms, std::bind(&MinimalPublisher::timer_callback, this));
  }

private:
  void timer_callback()
  {
    auto message = std_msgs::msg::String();
    message.data = "Hello, world! " + std::to_string(count_++);
    RCLCPP_INFO(this->get_logger(), "Publishing: '%s'", message.data.c_str());
    publisher_->publish(message);
  }
  rclcpp::TimerBase::SharedPtr timer_;
  rclcpp::Publisher<std_msgs::msg::String>::SharedPtr publisher_;
  size_t count_;
};

int main(int argc, char * argv[])
{
  rclcpp::init(argc, argv);
  rclcpp::spin(std::make_shared<MinimalPublisher>());
  rclcpp::shutdown();
  return 0;
}
```
</TabItem>
</Tabs>
