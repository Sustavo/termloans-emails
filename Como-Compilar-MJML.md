# Como Compilar Arquivos MJML para HTML

## O que é MJML?

MJML (Mailjet Markup Language) é uma linguagem de marcação criada para simplificar a criação de emails responsivos. Ela gera HTML compatível com diferentes clientes de email.

## Pré-requisitos

1. **Node.js**: Certifique-se de ter o Node.js instalado
2. **MJML CLI**: Instale globalmente ou use npx

### Instalação do MJML

```bash
# Instalação global
npm install -g mjml

# Ou usar diretamente com npx (recomendado)
npx mjml
```

## Estrutura Básica MJML

```mjml
<mjml>
  <mj-head>
    <mj-title>Título do Email</mj-title>
    <mj-attributes>
      <mj-all font-family="Arial, sans-serif" />
    </mj-attributes>
  </mj-head>
  <mj-body>
    <mj-section>
      <mj-column>
        <mj-text>Conteúdo do email</mj-text>
      </mj-column>
    </mj-section>
  </mj-body>
</mjml>
```

## Compilação

### Comando Básico

```bash
# Compilar arquivo específico
npx mjml input.mjml -o output.html

# Compilar com caminho completo
npx mjml "pasta/arquivo.mjml" -o "pasta/arquivo.html"
```

### Opções de Compilação

```bash
# Compilar com validação rigorosa
npx mjml input.mjml -o output.html --config.validationLevel=strict

# Compilar múltiplos arquivos
npx mjml pasta/*.mjml -o pasta-saida/

# Assistir mudanças (recompila automaticamente)
npx mjml input.mjml -o output.html --watch
```

## Regras Importantes de Estrutura

### ✅ Estrutura Correta
- `mj-section` deve estar diretamente dentro de `mj-body`
- `mj-column` deve estar dentro de `mj-section`
- `mj-text`, `mj-image`, etc. devem estar dentro de `mj-column`

### ❌ Erros Comuns
- **Não** coloque `mj-section` dentro de `mj-column`
- **Não** coloque `mj-body` dentro de `mj-column`
- **Não** use atributos CSS não suportados

### Exemplo de Correção

**Incorreto:**
```mjml
<mj-column>
  <mj-section> <!-- ERRO: section dentro de column -->
    <mj-column>
      <mj-text>Texto</mj-text>
    </mj-column>
  </mj-section>
</mj-column>
```

**Correto:**
```mjml
<mj-section>
  <mj-column>
    <mj-text>Texto</mj-text>
  </mj-column>
</mj-section>
```

## Resolução de Problemas

### Mensagens de Erro Comuns

1. **"mj-section cannot be used inside mj-column"**
   - Mova `mj-section` para fora da `mj-column`
   - Reorganize a estrutura seguindo a hierarquia correta

2. **"Attributes X are illegal"**
   - Verifique se o atributo é suportado pelo componente
   - Use CSS customizado em `mj-style` se necessário

3. **"mj-body cannot be used inside mj-column"**
   - `mj-body` deve ser o elemento raiz após `mj-head`
   - Não pode ser aninhado dentro de outros componentes

### Validação

```bash
# Validar sem compilar
npx mjml input.mjml --validate

# Compilar com validação rigorosa
npx mjml input.mjml -o output.html --config.validationLevel=strict
```

## Exemplo Prático

Dado o arquivo `email.mjml`:

```bash
# Compilar
npx mjml email.mjml -o email.html

# Compilar com validação
npx mjml email.mjml -o email.html --config.validationLevel=strict

# Assistir mudanças
npx mjml email.mjml -o email.html --watch
```

## Dicas

1. **Sempre valide** a estrutura antes de compilar
2. **Use CSS customizado** em `mj-style` para estilos avançados
3. **Teste em múltiplos clientes** de email
4. **Mantenha a hierarquia** de componentes correta
5. **Use paths relativos** para imagens quando possível

## Recursos Úteis

- [Documentação oficial MJML](https://mjml.io/documentation/)
- [Editor online MJML](https://mjml.io/try-it-live)
- [Componentes MJML](https://mjml.io/documentation/#components)