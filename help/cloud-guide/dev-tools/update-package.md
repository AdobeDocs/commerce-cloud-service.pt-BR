---
title: Atualize o pacote ECE-Tools
description: Saiba como atualizar o pacote ECE-Tools para aproveitar as correções e os recursos mais recentes aplicados ao Adobe Commerce na infraestrutura em nuvem.
feature: Cloud, Upgrade
exl-id: 7cce45eb-ae53-4468-b16d-4f4d3422ac52
source-git-commit: 513bc5b52f046ffd98005d80f34725b7f60b38bd
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---

# Atualize o pacote ECE-Tools

Uma atualização do `ece-tools` O pacote também atualiza o outro [Pacote de ferramentas na nuvem para pacotes do Commerce](../release-notes/cloud-tools-suite.md), que são dependências de `ece-tools`. Portanto, você deve usar uma versão do Adobe Commerce na infraestrutura em nuvem compatível com `ece-tools` pacote.

{{ece-tools-package}}

**Pré-requisitos**:

- Antes de atualizar `ece-tools`, revise a [Notas de versão do Cloud Tools Suite for Commerce](../release-notes/cloud-tools-suite.md).
- Se estiver atualizando a partir de `ece-tools` 2002.0.22 ou anterior a 2002.1.0, analisar [Alterações incompatíveis com versões anteriores](../release-notes/backward-incompatible-changes.md) e faça as alterações necessárias no projeto de infraestrutura do Adobe Commerce na nuvem.
- Revisão [Atualizações e patches](../development/commerce-version.md#upgrade-from-older-versions) para determinar as versões das ECE-Tools compatíveis com o seu projeto Adobe Commerce na infraestrutura em nuvem.

{{upgrade-tip}}

**Para atualizar o `ece-tools` pacote**:

1. Na estação de trabalho local, execute uma atualização usando o Composer.

   ```bash
   composer update magento/ece-tools --with-dependencies
   ```

   >[!NOTE]
   >
   >Se não for possível atualizar além de `ece-tools` versão 2002.0.8, consulte [Atualizar projeto para usar o pacote ECE-Tools](install-package.md).

1. Adicionar, confirmar e enviar alterações de código.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Update magento/ece-tools"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. Após a validação do teste, mescle essa ramificação à ramificação de integração.
