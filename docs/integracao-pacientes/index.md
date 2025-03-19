# Integração de pacientes

## 1. Introdução

A API de Integração de Pacientes tem como objetivo permitir que sistemas terceiros integrem e gerenciem informações básicas de pacientes de forma segura e eficiente com o sistema da Lya. Esta documentação fornece detalhes sobre como utilizar a API, incluindo sua finalidade, estrutura e formatos de resposta.

## 2. Objetivo

A API foi desenvolvida para possibilitar a recuperação de dados dos pacientes utilizando o padrão FHIR (Fast Healthcare Interoperability Resources), garantindo a interoperabilidade e padronização das informações de saúde. Com essa integração, os dados dos pacientes podem ser acessados e exibidos no sistema Lya durante os atendimentos, facilitando a análise histórica de informações médicas e auxiliando os profissionais de saúde na tomada de decisão. Dessa forma, a API contribui para um atendimento mais ágil e preciso, permitindo a identificação de diagnósticos com mais assertividade.

## 3. Estrutura da Documentação

Para facilitar a compreensão e implementação da API, a documentação está organizada da seguinte forma:

* **Informações Gerais:** Contém detalhes básicos sobre a API, como URL base, formato das respostas e versão.
* **Autenticação:** Explica os mecanismos de autenticação necessários para acessar a API de forma segura com exemplos.
* **Serviços, endpoints e suas funcionalidades:** Descreve os endpoints disponíveis para cada serviço, suas funcionalidades e exemplos de requisição e resposta.

## 4. Estrutura dos Serviços

A API de Integração de Pacientes é composta por diferentes serviços que atuam de forma integrada para garantir a segurança e eficiência na gestão dos dados. Abaixo estão os principais serviços envolvidos:

### 4.1. Lya Tenants

Serviço responsável por gerenciar os acessos à API, assegurando que apenas aplicações autorizadas possam utilizá-la. Esse serviço gerencia e verifica permissões e credenciais antes de conceder acesso aos recursos da API.

[Documentação do Lya Tenants](/doc/lya-tenants-g7JlwX8S4g)

### 4.2. Lya Patients

Serviço dedicado à criação e gerenciamento de adaptadores de autenticação para os serviços dos clientes. Ele permite que a Lya utilize as credenciais configuradas para autenticar-se nos sistemas do cliente e recuperar os dados dos pacientes de maneira segura e eficiente.

[Documentação do Lya Patients](/doc/lya-patients-d9eocmlTKa)

### 4.3. Lya API

Serviço principal da integração, responsável pelo gerenciamento dos pacientes dentro do sistema. Os pacientes cadastrados por meio desse serviço estarão disponíveis na Lya, permitindo que os profissionais de saúde os selecionem e realizem atendimentos diretamente pela plataforma.

[Documentação do Lya API](/doc/lya-api-7YecitI3Kc)

## 5. Definição da API

A API de Integração de Pacientes da Lya foi desenvolvida para permitir a comunicação eficiente e segura entre sistemas terceiros e os serviços oferecidos pela plataforma. Ela disponibiliza endpoints que possibilitam a recuperação, o gerenciamento e a autenticação de dados de pacientes, garantindo a interoperabilidade através do padrão **FHIR (Fast Healthcare Interoperability Resources)**.

### Endpoints Disponíveis

A API conta com uma variedade de endpoints organizados por serviço, incluindo **Lya Tenants**, **Lya Patients** e **Lya API**. Todos os detalhes sobre os endpoints, suas funcionalidades e exemplos de requisição podem ser acessados através do link abaixo:

🔗 [Documentação completa dos endpoints](../api.md)

A documentação técnica completa fornece instruções detalhadas sobre cada endpoint, incluindo parâmetros, códigos de resposta e exemplos de uso.

## 6. Contato e Suporte

Em caso de dúvidas ou problemas, entre em contato com o suporte [clicando aqui](https://lyahealth.com.br/contato).
