# Namespace
Namespace - механизм для разделения кластера k8s на несколько *виртуальных кластеров*.

Namespace это форма *мягкой изоляции (soft isolation)*, которая помогает организовывать *мягкую многотенантность (soft multi-tenancy)*. Для каждого Namespace можно применять различные квоты и политики.

**Тенант** - это широкое понятие, которое может обозначать отдельное приложение, различные команды или департаменты внутри компании, внешних потребителей.

Частый сценарий использования Namespaces - это разделение кластера на тенанты внутри одной организации. При этом объекты из одного Namespace могут влиять на объекты другого. Для более строгой изоляции используют несколько кластеров, каждый из которых запущен на отдельном оборудовании.

Объекты в k8s разделяются на те, которые могут принадлежать к Namespace *(namespaced objects)*, и на те, которые принадлежат к всему кластеру *(cluster-scoped)*. Это можно узнать следующей командой:
``` bash
kubectl api-resources
```
По умолчанию k8s развёртывает все объекты в Namespace ```default```.

Каждый кластер k8s имеет несколько заранее созданный системных Namespaces:
- default. В нём создаются все новые объекты, если при их создании не был указан Namespace
- kube-system. В нём располагаются компоненты Control plane (внутренний DNS сервер, сервер метрик и т. д.)
- kube-public. В нем располагаются объекты, которые должны быть доступны всем
- kube-node-lease. Node heart beat и *managing node leases (???)*

#### Некоторые команды
- Получить информацию про Namespace:
  ```bash
kubectl describe ns default
  ```
- К командам kubectl можно добавить параметр ```-n```, чтобы отфильтровать результат по Namespace (или ```--all-namespaces```, чтобы вернуть объекты из всех Namespaces). Получить все Services в kube-system Namespace:
  ``` bash
kubectl get svc --namespace kube-system
  ```
- Настроить kubeconfig, чтобы все последующие команды kubectl выполнялись для определённого Namespace:
  ```bash
kubectl config set-context --current --namespace mysupernamespace
  ```

Чтобы при декларативном создании объекта отнести его к определённому Namespace, необходимо указать название Namespace в поле ```metadata.namespace```:
``` yaml
apiVersion: v1
kind: Pod
metadata:
  namespace: mysupernamespace
  name: mysuperpod
...
```