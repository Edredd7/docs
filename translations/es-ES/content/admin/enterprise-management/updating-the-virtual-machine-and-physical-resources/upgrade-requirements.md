---
title: Requisitos de actualización
intro: 'Antes de actualizar el {% data variables.product.prodname_ghe_server %}, revisa estas recomendaciones y requisitos para planificar tu estrategia de actualización.'
redirect_from:
  - /enterprise/admin/installation/upgrade-requirements
  - /enterprise/admin/guides/installation/finding-the-current-github-enterprise-release
  - /enterprise/admin/enterprise-management/upgrade-requirements
  - /admin/enterprise-management/upgrade-requirements
  - /enterprise/admin/guides/installation/about-upgrade-requirements
versions:
  ghes: '*'
type: reference
topics:
  - Enterprise
  - Upgrades
---

{% note %}

**Notas:**
{% ifversion ghes < 3.3 %}- Las características tales como {% data variables.product.prodname_actions %}, {% data variables.product.prodname_registry %}, {% data variables.product.prodname_mobile %} y {% data variables.product.prodname_GH_advanced_security %} se encuentran disponibles en {% data variables.product.prodname_ghe_server %} 3.0 o superior. Te recomendamos ampliamente actualizar a la versión 3.0 o superior de los lanzamientos para que tengas todas las ventajas de las actualizaciones de seguridad, correcciones de errores y mejoras de características.{% endif %}
- Los paquetes de actualización están disponibles en [enterprise.github.com](https://enterprise.github.com/releases) para las versiones admitidas. Verifica la disponibilidad de los paquetes de actualización, deberás completar la actualización. Si un paquete no está disponible, contacta a {% data variables.contact.contact_ent_support %} para obtener ayuda.
- Si estás usando una Agrupación del {% data variables.product.prodname_ghe_server %}, consulta "[Actualizar una agrupación](/enterprise/admin/guides/clustering/upgrading-a-cluster/)" en la Guía de Agrupación del {% data variables.product.prodname_ghe_server %} para obtener instrucciones específicas únicas para agrupaciones.
- Estas notas de lanzamiento para el {% data variables.product.prodname_ghe_server %} brindan una lista detallada de las nuevas características de cada versión del {% data variables.product.prodname_ghe_server %}. Para obtener más información, consulta las [páginas de lanzamiento](https://enterprise.github.com/releases).

{% endnote %}

## Recomendaciones

- Incluye tantas nuevas actualizaciones como sea posible en tu proceso de actualización. Por ejemplo, en lugar de actualizar desde {% data variables.product.prodname_enterprise %} {{ enterpriseServerReleases.supported[2] }} a {{ enterpriseServerReleases.supported[1] }} a {{ enterpriseServerReleases.latest }}, podrías actualizar desde {% data variables.product.prodname_enterprise %} {{ enterpriseServerReleases.supported[2] }} a {{ enterpriseServerReleases.latest }}. Utiliza el [{% data variables.enterprise.upgrade_assistant %}](https://support.github.com/enterprise/server-upgrade) para encontrar la ruta de mejora desde tu versión de lanzamiento actual.
- Si estás varias versiones desactualizado, actualiza {% data variables.product.product_location %} tanto como sea posible con cada paso de tu proceso de actualización. Utilizar la versión más reciente posible en cada actualización te permite aprovechar las mejoras de desempeño y las correcciones de errores. Por ejemplo, podrías actualizar desde {% data variables.product.prodname_enterprise %} 2.7 a 2.8 a 2.10, pero actualizar desde {% data variables.product.prodname_enterprise %} 2.7 a 2.9 a 2.10 utiliza una versión posterior en el segundo paso.
- Utiliza el lanzamiento de patch más reciente cuando actualices. {% data reusables.enterprise_installation.enterprise-download-upgrade-pkg %}
- Utiliza una instancia de preparación para probar los pasos de actualización. Para obtener más información, consulta "[Configurar una instancia de preparación](/enterprise/admin/guides/installation/setting-up-a-staging-instance/)."
- Cuando ejecutas varias mejoras, espera por lo menos 24 horas entre las mejoras a las características para permitir que se completen totalmente las migraciones de datos y actualizaciones de las tareas que se ejecutan en segundo plano.
- Toma una captura de pantalla antes de que mejores tu máquina virtual. Para obtener más información, consulta "[Tomar una instantánea](/admin/enterprise-management/updating-the-virtual-machine-and-physical-resources/upgrading-github-enterprise-server#taking-a-snapshot)."
- Asegúrate de que tienes un respaldo reciente y exitoso de tu instancia. Para obtener más información, consulta el archivo README.md en [{% data variables.product.prodname_enterprise_backup_utilities %}](https://github.com/github/backup-utils#readme).

## Requisitos

- Debes actualizar desde una característica de lanzamiento que sea **como máximo** dos lanzamientos anteriores. Por ejemplo, para actualizar a {% data variables.product.prodname_enterprise %} {{ enterpriseServerReleases.latest }}, debes estar en {% data variables.product.prodname_enterprise %} {{ enterpriseServerReleases.supported[1] }} o {{ enterpriseServerReleases.supported[2] }}.
- Cuando hagas una mejora mediante un paquete de mejora, programa una ventana de mantenimiento para los usuarios finales de {% data variables.product.prodname_ghe_server %}.
- {% data reusables.enterprise_installation.hotpatching-explanation %}
- Es posible que un hotpatch requiera tiempo de inactividad si los servicios afectados (como kernel, MySQL, o Elasticsearch) requieren un reinicio de VM o un reinicio del servicio. Se te notificará cuando se necesite reiniciar. Puedes completar el reinicio más tarde.
- Es necesario que haya un almacenamiento raíz adicional disponible cuando se actualiza a través de un hotpatch, ya que instala múltiples versiones de determinados servicios hasta que se completa la actualización. El control de prevuelo te notificará si no tienes suficiente almacenamiento de disco raíz.
- Cuando se actualiza a través de un hotpatch, tu instancia no puede estar muy cargada, ya que puede impactar el proceso del hotpatch.
- Actualizar a {% data variables.product.prodname_ghe_server %} 2.17 migra tus registros de auditoría desde Elasticsearch a MySQL. Esta migración también incrementa la cantidad de tiempo y el espacio en disco que lleva restaurar una instantánea. Antes de migrar, controla el número de bytes en tus índices de registro de auditoría de ElasticSearch con este comando:
``` shell
curl -s http://localhost:9201/audit_log/_stats/store | jq ._all.primaries.store.size_in_bytes
```
Utiliza el número para estimar la cantidad de espacio de disco que los registros de auditoría de MySQL necesitarán. El script también controla tu espacio libre en disco mientras la importación está en progreso. Controlar este número es especialmente útil si tu espacio libre en disco está cerca de la cantidad de espacio en disco necesaria para la migración.

{% data reusables.enterprise_installation.upgrade-hardware-requirements %}

## Pasos siguientes

Después de revisar estas recomendaciones y requisitos, puedes actualizar el {% data variables.product.prodname_ghe_server %}. Para obtener más información, consulta "[Actualizar {% data variables.product.prodname_ghe_server %}](/enterprise/admin/guides/installation/upgrading-github-enterprise-server/)."
