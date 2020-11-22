# Programação Orientada a Objetos

## Trabalho 1: Princípio da Responsabilidade Única


#### Autor: Felipe Alves Cordeiro 744335
#### Princípio da Responsabilidade Única


## O Que é o Princípio da Responsabilidade Única?

O princípio da responsabilidade única é um dos princípios da orientação a objetos, este princípio é diretamente ligado a conceitos como acoplamento e coesão, ele parte da seguinte idéia citada primeiramente por Robert C. Martin em um de seus artigos: “O princípio de responsabilidade única afirma que cada módulo ou classe deve ter responsabilidade sobre uma única parte da funcionalidade fornecida pelo software, e essa responsabilidade deve ser totalmente encapsulada pela classe. Todos os seus serviços devem estar estreitamente alinhados com essa responsabilidade”.

Descrevendo o princípio de outra forma, uma classe ou componente deve buscar tratar somente de uma ideia ou conceito em principal, não deve ser algo que, por exemplo, faça uma alteração em uma interface de pagamento e também consiga gerar uma mudança no banco de dados dos usuários, a menos, é claro,  que esses dois pontos sejam extremamente ligados na lógica do software em questão. 

O princípio da responsabilidade única também é importante no quesito de manutenibilidade do código, isso pois uma classe muitas vezes é criada para ser utilizada em diversas outras, e quando esta precisa ser alterada as demais também precisarão ser retestadas e corrigidas se necessário. Porém ao seguir este princípio, o número de instâncias do código dependentes de uma mesma classe se reduz consideravelmente e com isso além de ter um objetivo bem claro para cada classe os testes do software após uma alteração também serão reduzidos.
 
## Exemplo de código com conceito não aplicado

O contexto do exemplo a seguir é de um aplicativo no qual o usuário consegue efetuar compras e vendas de criptomoedas. Quando o usuário decide comprar uma quantia de uma determinada moeda uma ordem de compra é enviada para o mercado, esta ordem permanecerá no mercado até que alguem venda a moeda por aquele mesmo valor. Cada moeda possui seus próprios valores e carteiras separadas.


```python

class criptoCoin:		

	def __init__(self, criptoName):
		self.criptoName=criptoName
		self.criptoWallet=0

	def updateWallet():
		print("Atualiza carteira")

	def placeBuyOrder(): 
		print("Insere ordem de compra")

	def placeSellOrder():
		print("Insere ordem de venda")

	def updateOrderStatus():
		print("Atualiza status de uma ordem")

	def showCurrentOrder():
		print("Mostra ordem para o usuario")

	def showCriptoWallet():
		print("Mostra saldo do cripto atual")

	def sendOrderToMarket():
		print("Enviando ordem para o mercado de ordens")

	def verifyMarketOrder():
		print("Verificando se ordem foi concluida")

	def cancelOrder():
		print("Cancela ordem")
		
```

No exemplo acima existe uma classe na qual é responsável por tratar tudo que ocorre com determinada moeda para um determinado usuário.  A partir desta classe é possível desde imprimir os dados na tela, quanto guardar o saldo da moeda atual ou enviar uma ordem para o mercado de ordens. 

A princípio pode parecer que a classe possui somente uma responsabilidade que seria sobre as ações para uma moeda em específico,  isso implica em ações em diferentes “áreas” da aplicação como a seção de interface do usuário e envio de dados para uma API que trata do mercado das moedas. Entretanto é exatamente neste ponto que a classe fere o princípio da responsabilidade única pois ela possui responsabilidades com a interface gráfica, com uma API externa, com a administração do saldo de uma criptomoeda e com as solicitações do usuário para inserir ou remover determinada ordem.

## Exemplo de código com conceito aplicado

Na imagem abaixo o contexto é o mesmo do exemplo anterior, com as mesmas funções porém rearrajandas para condizirem com o princípio da responsabilidade única.


```python

class criptoShow():

	def showCurrentOrder():
		print("Mostra ordem para o usuario")

	def showCriptoWallet():
		print("Mostra saldo do cripto atual")

class criptoMarket():

	def sendOrderToMarket():
		print("Enviando ordem para o mercado de ordens")

	def verifyMarketOrder():
		print("Verificando se ordem foi concluida")

class criptoOrder():

	def placeBuyOrder(): 
		print("Insere ordem de compra")

	def placeSellOrder():
		print("Insere ordem de venda")

	def updateOrderStatus():
		print("Atualiza status de uma ordem")

	def cancelOrder():
		print("Cancela ordem")

class criptoCoin():

	def __init__(self, criptoName):
		self.criptoName=criptoName
		self.criptoWallet=0

	def updateWallet():
		print("Atualiza carteira")

```

No código acima é possível observar que foram criadas 3 novas classes, foi criada a “CriptoShow” para tratar somente de interações com a interface, a “criptoMarket” para tratar somente com as trocas de informações com a API do mercado de ordens, a “criptoOrder” para administrar as solicitações vinculadas as ordens do usuário e por fim foi criada uma outra classe para guardar os dados da criptomoeda do usuário em questão. Com estas modificações é possível observar que o software ainda possui as mesmas funções porém organizadas em diferentes classes de forma que estas possuam somente uma responsabilidade.


### Referências:

https://deviq.com/single-responsibility-principle/

https://medium.com/desenvolvendo-com-paixao/o-que-%C3%A9-solid-o-guia-completo-para-voc%C3%AA-entender-os-5-princ%C3%ADpios-da-poo-2b937b3fc530