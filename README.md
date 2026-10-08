# NDD Printer M-Manager

Userscript para o **NDD Print Portal 360** (`https://360.nddprint.com/printers`) que adiciona um painel de gestão em massa da lista de impressoras.

## Instalação

1. Instale uma extensão de userscripts: [Tampermonkey](https://www.tampermonkey.net/) ou [Violentmonkey](https://violentmonkey.github.io/).
2. Abra o link abaixo. A extensão mostra a tela de instalação; confirme em **Instalar**.

   **[Instalar o NDD Printer M-Manager](https://raw.githubusercontent.com/maiconjs/ndd-printer-m-manager/main/ndd-printer-m-manager.user.js)**

3. Acesse `https://360.nddprint.com/printers` (ou recarregue a página). O painel aparece no canto da tela.

No Chrome/Edge com Tampermonkey, pode ser necessário ativar o **Modo do desenvolvedor** em `chrome://extensions` (ou "Permitir scripts de usuário" nos detalhes da extensão) para os scripts rodarem.

### Atualizações

O script declara `@updateURL`/`@downloadURL` apontando para este repositório: a extensão verifica novas versões sozinha (ou manualmente em *Verificar atualizações*). Uma versão nova só é oferecida quando o número em `@version` aumenta.

## Recursos

- **Seleção em massa**: visíveis, todas as páginas, portas USB, impressoras sem fila, por fabricante/modelo, com janela de revisão e filtros por coluna no estilo Excel.
- **Contabilização em lote**: status, origem (Padrão do sistema, Física e Lógica, Apenas Lógica, Apenas Física com MF/Client Collector) e forçar cor. Escolher uma origem com o status em "manter" habilita as impressoras desabilitadas na mesma gravação.
- **Coluna Origem**: coleta sob demanda, com cache por cliente conferido pela auditoria do NDD (só relê o que mudou).
- **Lista de séries (contrato)**: carrega `.csv`/`.txt`, compara com todas as impressoras do NDD, destaca as que estão fora da lista e as séries da lista que não existem no NDD.
- **Exclusão em massa**: desabilita a contabilização e exclui, acompanhando a fila de liberação do servidor.
- **Ambiente**: filas de impressão por impressora e janela de hosts/produtos NDD com situação de comunicação.
- **Grade**: colunas redimensionáveis com larguras lembradas, exportação `.csv` (abre direto no Excel) e log persistente até fechar a aba.

## Observações

- Usa a mesma sessão do portal (as chamadas à API são feitas com o login atual); não armazena credenciais.
- Ações que alteram dados (contabilização e exclusão) sempre pedem confirmação e registram o resultado no log.
- Exclusão bloqueada por `@@360PrinterCounterStatusIsEnabled` depende de desabilitar o contador no NDD MPS; não há como fazer isso pelo Portal 360.
