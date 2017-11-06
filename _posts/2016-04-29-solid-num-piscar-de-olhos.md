---
layout: post
title:  SOLID num piscar de olhos
tags:
- PHP
- Padrões
---

<h2 id="1-Single Responsability">1 - Single Responsability</h2>

<p>Uma classe deve conter apenas uma responsabilidade. Deve-se extrair funcionalidades distintas em suas próprias classes, e fazer do sistema um conjunto de classes que interagem entre si. <em>"Programe para uma interface, não para uma implementação"</em> - defina as necessidades de sua classe por meio de interfaces. As implementações concretas destas interfaces devem se preocupar em como realizar e executar o trabalho específico.</p>

<h2 id="2-Open-losed">2 - Open-Closed (extensão/modificação)</h2>

<p>Entidades devem estar abertas para extensão, porém fechadas para modificação. O objetivo é ter entidades capazes de ampliar suas funcionalidades sem modificar o código fonte. Para alcançar este objetivo, substitua o comportamento que pode ser estendido por uma interface. Novamente <em>"Programe para uma interface, não para uma implementação"</em>.</p>


<h2 id="3-Liskov-Substitution">3 - Liskov Substitution</h2>

<p>Deve ser possível substituir uma classe por qualquer uma de suas subclasses. Se uma subclasse sobrescreve o comportamento de sua super-classe, ela não deve gerar uma implementação incoerente com a implementação da super-classe. Mantenha a coerência com a assinatura dos métodos nas subclasses (parâmetros, exceções lançadas, comportamento e tipo de retorno). </p>

<h2 id="4-Interface-Segregation">4 - Interface Segregation</h2>

<p>Uma classe não deve ser obrigada a implementar uma interface que ela não usa. Crie interfaces concisas e com responsabilidades bem definidas, para que seus clientes não sejam forçados a implementar funcionalidades que estão fora de sua realidade.</p>

<h2 id="5-Dependency-Inversion">5 - Dependency Inversion (not Dependency Injection)</h2>

<p>Considere código de baixo nível como classes que implementam operações primárias (acesso a disco, acesso à interface de rede, etc). Considere código de alto nível aquele que gerencia a lógica da aplicação.</p>
<p>Portanto, código de alto nível deve confiar em classes abstratas, não em classes de baixo nível concretas. A tendência natural é usar código de baixo nível diretamente em códigos de alto nível, adequando o código de alto nível às necessidades dos módulos de baixo nível. O problema é quando surge a necessidade de mudar a implementação do código de baixo nível ou até mesmo mudar a lógica do sistema, gerando problemas de manutenção.</p>
<p>Para evitar tais problemas, podemos introduzir uma camada de abstração entre as classes de alto nível e classes de baixo nível. Invertendo o controle, a nova camada de abstração não deve ser criado com base em módulos de baixo nível, mas módulos de baixo nível devem ser criados com base na camada de abstração, se adequando a camada de abstração, delegando o devido controle aos módulos de alto nível.</p>
