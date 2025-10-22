---
title: Serviços e Ações
sidebar_position: 4
slug: /ros-service
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';
import Admonition from '@theme/Admonition';

# Serviços e Ações

## 1. Serviços

![servico_gif](/gifs/servico.gif)

[fonte](https://docs.ros.org/en/humble/Tutorials/Beginner-CLI-Tools/Understanding-ROS2-Nodes/Understanding-ROS2-Nodes.html)

Os serviços no ROS 2 são uma forma essencial de comunicação entre os nós.
Diferentemente dos tópicos, que operam no modelo de publicação-subscrição, os
serviços funcionam com base em um modelo de chamada e resposta. Isso significa
que, enquanto os tópicos permitem que os nós se inscrevam em fluxos de dados e
recebam atualizações contínuas, os serviços fornecem dados apenas quando são
especificamente chamados por um cliente. Aqui está um guia sobre como os
serviços funcionam no ROS 2:

### 1.1. Configuração
Para começar, você deve iniciar os nós do turtlesim e do turtle_teleop_key:
```
ros2 run turtlesim turtlesim_node
ros2 run turtlesim turtle_teleop_key
```

### 1.2. Listando Serviços
Para listar todos os serviços ativos no sistema, use o comando:
```
ros2 service list
```

### 1.3. Verificando o Tipo de Serviço
Cada serviço tem um tipo que descreve a estrutura dos dados de solicitação e
resposta. Para descobrir o tipo de um serviço,
use:
```
ros2 service type <nome_do_serviço>
```
Por exemplo, para o serviço `/clear`, o tipo é `std_srvs/srv/Empty`, indicando
que não envia ou recebe
dados.

### 1.4. Encontrando Serviços por Tipo
Se você quiser encontrar todos os serviços de um tipo específico, use:
```
ros2 service find <tipo_do_serviço>
```

### 1.5. Mostrando a Estrutura do Serviço
Para entender a estrutura dos argumentos de entrada de um serviço, use:
```
ros2 interface show <tipo_do_serviço>
```
Por exemplo, para o serviço `/spawn`, a estrutura inclui `x`, `y`, `theta` e
`name`.

### 1.6. Chamando um Serviço
Agora que você conhece a estrutura dos argumentos, pode chamar um serviço
usando:
```
ros2 service call <nome_do_serviço> <tipo_do_serviço> <argumentos>
```
Por exemplo, para chamar o serviço `/spawn` e criar uma nova tartaruga, use:
```
ros2 service call /spawn turtlesim/srv/Spawn "{x: 2, y: 2, theta: 0.2, name: ''}"
```

## 2. Ações

![](/gifs/acoes.gif)

Ações no ROS 2 são um tipo de comunicação destinado a tarefas de longa duração.
Elas são compostas por três partes: um objetivo (goal), feedback e um resultado
(result). As ações são construídas sobre tópicos e serviços, oferecendo
funcionalidades semelhantes aos serviços, mas com a capacidade de serem
canceladas e fornecerem feedback
contínuo.

### 2.1. Configuração
Antes de começar a trabalhar com ações, você precisa ter o ROS 2 e o pacote
turtlesim instalados. Inicie os nós do turtlesim e do
turtle_teleop_key:
```
ros2 run turtlesim turtlesim_node
ros2 run turtlesim turtle_teleop_key
```

### 2.2. Usando Ações
Quando você inicia o nó /teleop_turtle, ele permite que você mova a tartaruga
usando as teclas de seta e execute ações usando outras teclas. Por exemplo, as
teclas G, B, V, C, D, E, R, T permitem que você rotacione a tartaruga para
orientações específicas. A tecla F cancela uma rotação em
andamento.

### 2.3. Informações do Nó
Para ver a lista de ações que um nó fornece, use o comando `ros2 node info`. Por
exemplo:
```
ros2 node info /turtlesim
```
Isso retornará uma lista de assinantes, publicadores, serviços, servidores de
ação e clientes de ação do nó
/turtlesim.

### 2.4. Listando Ações
Para listar todas as ações ativas no sistema, use o comando:
```
ros2 action list
```
Para ver os tipos de ações, adicione a opção `-t`:
```
ros2 action list -t
```

### 2.5. Informações sobre uma Ação
Para obter informações sobre uma ação específica, como o número de clientes e
servidores de ação, use o
comando:
```
ros2 action info <nome_da_ação>
```

### 2.6. Estrutura da Ação
Para ver a estrutura de um tipo de ação, use o comando:
```
ros2 interface show <tipo_da_ação>
```
Isso mostrará a estrutura dos objetivos, resultados e feedback da ação.

### 2.7. Enviando um Objetivo para uma Ação
Para enviar um objetivo para uma ação, use o comando:
```
ros2 action send_goal <nome_da_ação> <tipo_da_ação> <valores>
```
Você pode adicionar a opção `--feedback` para ver o feedback contínuo da ação.

## 3. Exemplos

### 3.1. Serviços 

Vamos criar dois arquivos, um para o server e outro para o client:

```bash
touch ros_server.py ros_client.py
chmod +x ros_server.py ros_client.py
```

O conteúdo dos dois arquivos pode ser visto abaixo:

<Tabs defaultValue="server" values={[
        {label: 'Servidor', value: 'server'},
        {label: 'Cliente', value: 'client'},
  ]}>

<TabItem value="server">

```python showLineNumbers title="ros_server.py"
from example_interfaces.srv import AddTwoInts

import rclpy

g_node = None


def add_two_ints_callback(request, response):
    global g_node
    response.sum = request.a + request.b
    g_node.get_logger().info(
        'Incoming request\na: %d b: %d' % (request.a, request.b))

    return response


def main(args=None):
    global g_node
    rclpy.init(args=args)

    g_node = rclpy.create_node('minimal_service')

    srv = g_node.create_service(AddTwoInts, 'add_two_ints', add_two_ints_callback)
    while rclpy.ok():
        rclpy.spin_once(g_node)

    # Destroy the service attached to the node explicitly
    # (optional - otherwise it will be done automatically
    # when the garbage collector destroys the node object)
    g_node.destroy_service(srv)
    rclpy.shutdown()


if __name__ == '__main__':
    main()
```

</TabItem>

<TabItem value="client">

```python showLineNumbers title="ros_client.py"
from example_interfaces.srv import AddTwoInts

import rclpy


def main(args=None):
    rclpy.init(args=args)
    node = rclpy.create_node('minimal_client')
    cli = node.create_client(AddTwoInts, 'add_two_ints')

    req = AddTwoInts.Request()
    req.a = 41
    req.b = 1
    while not cli.wait_for_service(timeout_sec=1.0):
        node.get_logger().info('service not available, waiting again...')

    future = cli.call_async(req)
    rclpy.spin_until_future_complete(node, future)

    result = future.result()
    node.get_logger().info(
        'Result of add_two_ints: for %d + %d = %d' %
        (req.a, req.b, result.sum))

    node.destroy_node()
    rclpy.shutdown()


if __name__ == '__main__':
    main()
```

</TabItem>

</Tabs>

O vídeo abaixo exemplifica o comportamento dos dois scripts:

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/rY_ikKTlcSM"
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br />


:::tip Dica

Note que, para usar um serviço, você precisa utilizar um `request` disponível
nos módulos padrão do ROS ou em algum dos que tem instalado. Como um exemplo,
para ver a lista de requests relacionados ao turtlesim, podemos usar:

```bash
ls /opt/ros/humble/share/turtlesim*/**/*.srv
```

Basta substituir `turtlesim*` por qualquer pacote que exista no diretório
`/opt/ros/humble/share`

:::

### 3.2. Ações

Vamos criar dois arquivos, um para o server e outro para o client:

```bash
touch action_server.py action_client.py
chmod +x action_server.py action_client.py
```

O conteúdo dos dois arquivos pode ser visto abaixo:

<Tabs defaultValue="server" values={[
        {label: 'Servidor', value: 'server'},
        {label: 'Cliente', value: 'client'},
  ]}>

<TabItem value="server">

```python showLineNumbers title="action_server.py"
#! /usr/bin/env python3
import time

from example_interfaces.action import Fibonacci

import rclpy
from rclpy.action import ActionServer, CancelResponse, GoalResponse
from rclpy.callback_groups import ReentrantCallbackGroup
from rclpy.executors import MultiThreadedExecutor
from rclpy.node import Node


class MinimalActionServer(Node):

    def __init__(self):
        super().__init__('minimal_action_server')

        self._action_server = ActionServer(
            self,
            Fibonacci,
            'fibonacci',
            execute_callback=self.execute_callback,
            callback_group=ReentrantCallbackGroup(),
            goal_callback=self.goal_callback,
            cancel_callback=self.cancel_callback)

    def destroy(self):
        self._action_server.destroy()
        super().destroy_node()

    def goal_callback(self, goal_request):
        """Accept or reject a client request to begin an action."""
        # This server allows multiple goals in parallel
        self.get_logger().info('Received goal request')
        return GoalResponse.ACCEPT

    def cancel_callback(self, goal_handle):
        """Accept or reject a client request to cancel an action."""
        self.get_logger().info('Received cancel request')
        return CancelResponse.ACCEPT

    async def execute_callback(self, goal_handle):
        """Execute a goal."""
        self.get_logger().info('Executing goal...')

        # Append the seeds for the Fibonacci sequence
        feedback_msg = Fibonacci.Feedback()
        feedback_msg.sequence = [0, 1]

        # Start executing the action
        for i in range(1, goal_handle.request.order):
            if goal_handle.is_cancel_requested:
                goal_handle.canceled()
                self.get_logger().info('Goal canceled')
                return Fibonacci.Result()

            # Update Fibonacci sequence
            feedback_msg.sequence.append(feedback_msg.sequence[i] + feedback_msg.sequence[i-1])

            self.get_logger().info('Publishing feedback: {0}'.format(feedback_msg.sequence))

            # Publish the feedback
            goal_handle.publish_feedback(feedback_msg)

            # Sleep for demonstration purposes
            time.sleep(1)

        goal_handle.succeed()

        # Populate result message
        result = Fibonacci.Result()
        result.sequence = feedback_msg.sequence

        self.get_logger().info('Returning result: {0}'.format(result.sequence))

        return result


def main(args=None):
    rclpy.init(args=args)

    minimal_action_server = MinimalActionServer()

    # Use a MultiThreadedExecutor to enable processing goals concurrently
    executor = MultiThreadedExecutor()

    rclpy.spin(minimal_action_server, executor=executor)

    minimal_action_server.destroy()
    rclpy.shutdown()


if __name__ == '__main__':
    main()
```

</TabItem>

<TabItem value="client">

```python showLineNumbers title="action_client.py"
#! /usr/bin/env python3
from action_msgs.msg import GoalStatus
from example_interfaces.action import Fibonacci

import rclpy
from rclpy.action import ActionClient
from rclpy.node import Node


class MinimalActionClient(Node):

    def __init__(self):
        super().__init__('minimal_action_client')
        self._action_client = ActionClient(self, Fibonacci, 'fibonacci')

    def goal_response_callback(self, future):
        goal_handle = future.result()
        if not goal_handle.accepted:
            self.get_logger().info('Goal rejected :(')
            return

        self.get_logger().info('Goal accepted :)')

        self._get_result_future = goal_handle.get_result_async()
        self._get_result_future.add_done_callback(self.get_result_callback)

    def feedback_callback(self, feedback):
        self.get_logger().info('Received feedback: {0}'.format(feedback.feedback.sequence))

    def get_result_callback(self, future):
        result = future.result().result
        status = future.result().status
        if status == GoalStatus.STATUS_SUCCEEDED:
            self.get_logger().info('Goal succeeded! Result: {0}'.format(result.sequence))
        else:
            self.get_logger().info('Goal failed with status: {0}'.format(status))

        # Shutdown after receiving a result
        rclpy.shutdown()

    def send_goal(self):
        self.get_logger().info('Waiting for action server...')
        self._action_client.wait_for_server()

        goal_msg = Fibonacci.Goal()
        goal_msg.order = 10

        self.get_logger().info('Sending goal request...')

        self._send_goal_future = self._action_client.send_goal_async(
            goal_msg,
            feedback_callback=self.feedback_callback)

        self._send_goal_future.add_done_callback(self.goal_response_callback)


def main(args=None):
    rclpy.init(args=args)

    action_client = MinimalActionClient()

    action_client.send_goal()

    rclpy.spin(action_client)


if __name__ == '__main__':
    main()
```

</TabItem>

</Tabs>

O vídeo abaixo exemplifica o comportamento dos dois scripts:

<div style={{ textAlign: 'center' }}>
    <iframe 
        style={{
            display: 'block',
            margin: 'auto',
            width: '100%',
            height: '50vh',
        }}
        src="https://www.youtube.com/embed/b70Zud0zjRI"
        frameborder="0" 
        allowFullScreen>
    </iframe>
</div>
<br/>
