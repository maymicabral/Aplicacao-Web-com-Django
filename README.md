# Django: Autenticação e Formulários de Alerta

Este README documenta os principais conceitos e aprendizados do curso **"Django: Autenticação e Formulários de Alerta"**, com o objetivo de consolidar os conhecimentos adquiridos e servir como referência futura.

## Objetivos do Curso
Este curso faz parte da trilha **Python Web** e tem como foco:

- **Conhecer os módulos internos do Django** que permitem a criação de formulários;
- **Acessar o banco de dados interno** do Django;
- **Aprender a realizar validações** nos dados submetidos pelos formulários;
- **Implementar mensagens dinâmicas de alerta**, integradas à aplicação;
- **Estruturar partials** para evitar a repetição de códigos em templates.

---

## Conceitos e Técnicas Aprendidas

### 1. **Módulos Internos do Django para Formulários**
- Uso da classe **`forms.Form`** para criar formulários personalizados;
- Utilização dos widgets do Django para personalização de campos;
- Definição de validações adicionais através dos métodos **`clean`** e **`clean_<field>`**.

### 2. **Acesso ao Banco de Dados Interno**
- Manipulação dos modelos (models) associados a formulários;
- Uso de **formulários baseados em models** para integração automática com o banco de dados;
- Estruturação de **migrations** para gerenciar alterações no banco de dados.

### 3. **Validação de Dados**
- Implementação de validações customizadas para campos específicos;
- Aplicação de mensagens de erro dinâmicas para uma experiência de usuário aprimorada.

### 4. **Mensagens de Alerta Dinâmicas**
- Uso do framework de mensagens do Django (**`django.contrib.messages`**);
- Configuração de **categorias de mensagens** como `success`, `info`, `warning` e `error`;
- Exibição de mensagens no template utilizando loops e estruturas condicionais.

### 5. **Estruturação de Partials**
- Divisão de templates em componentes reutilizáveis;
- Uso da tag **`{% include %}`** para incorporar partials em templates maiores;
- Redução da duplicidade e aumento da manutenção do código.

---

## Exemplo de Implementação

### Configuração de Formulário com Validação
```python
from django import forms

class AlertaForm(forms.Form):
    titulo = forms.CharField(max_length=100, required=True, label='Título')
    descricao = forms.CharField(widget=forms.Textarea, required=True, label='Descrição')

    def clean_titulo(self):
        titulo = self.cleaned_data.get('titulo')
        if 'alerta' not in titulo.lower():
            raise forms.ValidationError('O título deve conter a palavra "alerta".')
        return titulo
```

### Exibição de Mensagens no Template
```html
{% if messages %}
    <ul class="mensagens">
        {% for message in messages %}
            <li class="{{ message.tags }}">{{ message }}</li>
        {% endfor %}
    </ul>
{% endif %}
```

### Exemplo de Partial
```html
<!-- partials/form.html -->
<form method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit">Enviar</button>
</form>
```

---

## Benefícios do Curso
- Melhoria na organização e manutenção do código Django;
- Domínio de técnicas para validação de dados e mensagens de alerta;
- Aprendizado prático na construção de aplicações web dinâmicas e seguras.

---

## Referências
- [Documentação Oficial do Django](https://docs.djangoproject.com/)
- [Curso na Alura](https://www.alura.com.br/)

---

## Autor
Este README foi elaborado como parte do processo de aprendizado no curso de Django. Para dúvidas ou sugestões, sinta-se à vontade para entrar em contato!

