# NUC KServe

Helm chart for rendering KServe custom resources from declarative values.

The chart does not install KServe CRDs or controllers. It only renders KServe objects that are already supported by the target cluster.

## Quick Start

Render the example configuration:

```bash
helm template nuc-kserve . -f values.yaml.example
```

Install the chart:

```bash
helm install nuc-kserve . \
  --namespace kserve \
  --create-namespace \
  -f values.yaml.example
```

Install the local README generator hook:

```bash
pre-commit install
pre-commit install-hooks
```

## Supported Resources

The chart can render these KServe kinds:

- `ClusterServingRuntime`
- `ClusterStorageContainer`
- `InferenceGraph`
- `InferenceService`
- `LocalModelCache`
- `LocalModelNodeGroup`
- `LocalModelNode`
- `ServingRuntime`
- `TrainedModel`

## Values Model

Each top-level list in [values.yaml](values.yaml) maps to one resource kind:

- `clusterServingRuntimes`
- `clusterStorageContainers`
- `inferenceGraphs`
- `inferenceServices`
- `localModelCaches`
- `localModelNodeGroups`
- `localModelNodes`
- `servingRuntimes`
- `trainedModels`

Every list item uses the same generic contract:

| Field | Required | Description |
|-------|----------|-------------|
| `enabled` | no | Set to `false` to keep a documented stub entry from rendering. |
| `name` | yes | Resource name. |
| `namespace` | no | Namespace for namespaced resources. Defaults to the Helm release namespace. Ignored for cluster-scoped kinds. |
| `labels` | no | Labels merged on top of built-in chart labels and `commonLabels`. |
| `annotations` | no | Annotations merged on top of `commonAnnotations`. |
| `apiVersion` | no | Per-resource API version override. |
| `spec` | no | Raw resource spec rendered as-is. |
| `status` | no | Optional raw status block. Usually useful only for fixtures. |

Global controls:

- `nameOverride`
- `commonLabels`
- `commonAnnotations`
- `apiVersions.*`

The value contract is validated by [values.schema.json](values.schema.json).

## Helm Values

This section is generated from [values.yaml](values.yaml) by `helm-docs`. Edit [values.yaml](values.yaml) comments or [docs/README.md.gotmpl](docs/README.md.gotmpl), then run `pre-commit run helm-docs --all-files` or `make docs` if you need to refresh it outside a commit.

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| apiVersions.clusterServingRuntime | string | `"serving.kserve.io/v1alpha1"` | Default apiVersion for ClusterServingRuntime resources. |
| apiVersions.clusterStorageContainer | string | `"serving.kserve.io/v1alpha1"` | Default apiVersion for ClusterStorageContainer resources. |
| apiVersions.inferenceGraph | string | `"serving.kserve.io/v1alpha1"` | Default apiVersion for InferenceGraph resources. |
| apiVersions.inferenceService | string | `"serving.kserve.io/v1beta1"` | Default apiVersion for InferenceService resources. |
| apiVersions.localModelCache | string | `"serving.kserve.io/v1alpha1"` | Default apiVersion for LocalModelCache resources. |
| apiVersions.localModelNode | string | `"serving.kserve.io/v1alpha1"` | Default apiVersion for LocalModelNode resources. |
| apiVersions.localModelNodeGroup | string | `"serving.kserve.io/v1alpha1"` | Default apiVersion for LocalModelNodeGroup resources. |
| apiVersions.servingRuntime | string | `"serving.kserve.io/v1alpha1"` | Default apiVersion for ServingRuntime resources. |
| apiVersions.trainedModel | string | `"serving.kserve.io/v1alpha1"` | Default apiVersion for TrainedModel resources. |
| clusterServingRuntimes | list | `[{"annotations":{},"apiVersion":"serving.kserve.io/v1alpha1","enabled":false,"labels":{},"name":"example-clusterservingruntime","spec":{"containers":[{"args":["--model_name={{.Name}}","--model_dir=/mnt/models"],"image":"example/runtime:latest","name":"kserve-container"}],"protocolVersions":["v1","v2"],"supportedModelFormats":[{"autoSelect":true,"name":"sklearn","priority":1,"version":"1"}]},"status":{}}]` | ClusterServingRuntime resources to render. |
| clusterServingRuntimes[0].annotations | object | `{}` | Additional resource annotations. |
| clusterServingRuntimes[0].apiVersion | string | `"serving.kserve.io/v1alpha1"` | Per-resource apiVersion override. |
| clusterServingRuntimes[0].enabled | bool | `false` | Set to `true` to render this resource. |
| clusterServingRuntimes[0].labels | object | `{}` | Additional resource labels. |
| clusterServingRuntimes[0].name | string | `"example-clusterservingruntime"` | Resource name. |
| clusterServingRuntimes[0].spec.containers[0].args | list | `["--model_name={{.Name}}","--model_dir=/mnt/models"]` | Runtime container arguments. |
| clusterServingRuntimes[0].spec.containers[0].image | string | `"example/runtime:latest"` | Runtime container image. |
| clusterServingRuntimes[0].spec.containers[0].name | string | `"kserve-container"` | Runtime container name. |
| clusterServingRuntimes[0].spec.protocolVersions | list | `["v1","v2"]` | Supported inference protocol versions. |
| clusterServingRuntimes[0].spec.supportedModelFormats[0].autoSelect | bool | `true` | Mark this format for autoselection. |
| clusterServingRuntimes[0].spec.supportedModelFormats[0].name | string | `"sklearn"` | Supported model format name. |
| clusterServingRuntimes[0].spec.supportedModelFormats[0].priority | int | `1` | Priority used when multiple runtimes support the same format. |
| clusterServingRuntimes[0].spec.supportedModelFormats[0].version | string | `"1"` | Supported model format version. |
| clusterServingRuntimes[0].status | object | `{}` | Optional synthetic status payload. |
| clusterStorageContainers | list | `[{"annotations":{},"apiVersion":"serving.kserve.io/v1alpha1","enabled":false,"labels":{},"name":"example-clusterstoragecontainer","spec":{"container":{"image":"example/storage-initializer:latest","imagePullPolicy":"IfNotPresent","name":"storage-initializer"},"supportedUriFormats":[{"prefix":"s3://"},{"regex":"https?://(.+)/(.+)"}],"workloadType":"initContainer"},"status":{}}]` | ClusterStorageContainer resources to render. |
| clusterStorageContainers[0].enabled | bool | `false` | Set to `true` to render this resource. |
| clusterStorageContainers[0].name | string | `"example-clusterstoragecontainer"` | Resource name. |
| clusterStorageContainers[0].spec.container.image | string | `"example/storage-initializer:latest"` | Storage initializer image. |
| clusterStorageContainers[0].spec.container.imagePullPolicy | string | `"IfNotPresent"` | Image pull policy for the storage initializer. |
| clusterStorageContainers[0].spec.container.name | string | `"storage-initializer"` | Storage initializer container name. |
| clusterStorageContainers[0].spec.supportedUriFormats[0].prefix | string | `"s3://"` | URI prefix handled by this storage container. |
| clusterStorageContainers[0].spec.supportedUriFormats[1].regex | string | `"https?://(.+)/(.+)"` | URI regex handled by this storage container. |
| clusterStorageContainers[0].spec.workloadType | string | `"initContainer"` | Workload type used by the storage container. |
| commonAnnotations | object | `{}` | Extra annotations applied to every rendered resource. |
| commonLabels | object | `{}` | Extra labels applied to every rendered resource. |
| inferenceGraphs | list | `[{"annotations":{},"apiVersion":"serving.kserve.io/v1alpha1","enabled":false,"labels":{},"name":"example-inferencegraph","namespace":"default","spec":{"nodes":{"root":{"routerType":"Sequence","steps":[{"serviceName":"predictor-a"},{"data":"$request","serviceName":"predictor-b"}]}}},"status":{}}]` | InferenceGraph resources to render. |
| inferenceGraphs[0].enabled | bool | `false` | Set to `true` to render this resource. |
| inferenceGraphs[0].name | string | `"example-inferencegraph"` | Resource name. |
| inferenceGraphs[0].namespace | string | `"default"` | Resource namespace. Defaults to the Helm release namespace. |
| inferenceGraphs[0].spec.nodes.root.routerType | string | `"Sequence"` | Router strategy used by the root node. |
| inferenceGraphs[0].spec.nodes.root.steps[0].serviceName | string | `"predictor-a"` | Downstream service name for a graph step. |
| inferenceGraphs[0].spec.nodes.root.steps[1].data | string | `"$request"` | Optional payload source for the next step. |
| inferenceServices | list | `[{"annotations":{},"apiVersion":"serving.kserve.io/v1beta1","enabled":false,"labels":{},"name":"example-inferenceservice","namespace":"default","spec":{"predictor":{"sklearn":{"storageUri":"s3://models/sklearn"}}},"status":{}}]` | InferenceService resources to render. |
| inferenceServices[0].enabled | bool | `false` | Set to `true` to render this resource. |
| inferenceServices[0].name | string | `"example-inferenceservice"` | Resource name. |
| inferenceServices[0].namespace | string | `"default"` | Resource namespace. Defaults to the Helm release namespace. |
| inferenceServices[0].spec.predictor.sklearn.storageUri | string | `"s3://models/sklearn"` | Model storage URI for the built-in sklearn predictor. |
| localModelCaches | list | `[{"annotations":{},"apiVersion":"serving.kserve.io/v1alpha1","enabled":false,"labels":{},"name":"example-localmodelcache","spec":{"modelSize":"10Gi","nodeGroups":["example-node-group"],"sourceModelUri":"s3://models/example"},"status":{}}]` | LocalModelCache resources to render. |
| localModelCaches[0].enabled | bool | `false` | Set to `true` to render this resource. |
| localModelCaches[0].name | string | `"example-localmodelcache"` | Resource name. |
| localModelCaches[0].spec.modelSize | string | `"10Gi"` | Estimated cached model size. |
| localModelCaches[0].spec.nodeGroups | list | `["example-node-group"]` | Target LocalModelNodeGroup names. |
| localModelCaches[0].spec.sourceModelUri | string | `"s3://models/example"` | Source model URI. |
| localModelNodeGroups | list | `[{"annotations":{},"apiVersion":"serving.kserve.io/v1alpha1","enabled":false,"labels":{},"name":"example-localmodelnodegroup","spec":{"persistentVolumeClaimSpec":{"accessModes":["ReadWriteOnce"],"resources":{"requests":{"storage":"20Gi"}},"storageClassName":"standard"},"persistentVolumeSpec":{"accessModes":["ReadWriteOnce"],"capacity":{"storage":"20Gi"},"hostPath":{"path":"/var/lib/kserve/localmodel"},"persistentVolumeReclaimPolicy":"Delete"},"storageLimit":"100Gi"},"status":{}}]` | LocalModelNodeGroup resources to render. |
| localModelNodeGroups[0].enabled | bool | `false` | Set to `true` to render this resource. |
| localModelNodeGroups[0].name | string | `"example-localmodelnodegroup"` | Resource name. |
| localModelNodeGroups[0].spec.persistentVolumeClaimSpec.accessModes | list | `["ReadWriteOnce"]` | PersistentVolumeClaim access modes. |
| localModelNodeGroups[0].spec.persistentVolumeClaimSpec.resources.requests.storage | string | `"20Gi"` | Requested PVC storage size. |
| localModelNodeGroups[0].spec.persistentVolumeClaimSpec.storageClassName | string | `"standard"` | PVC storage class name. |
| localModelNodeGroups[0].spec.persistentVolumeSpec.accessModes | list | `["ReadWriteOnce"]` | Backing PersistentVolume access modes. |
| localModelNodeGroups[0].spec.persistentVolumeSpec.capacity.storage | string | `"20Gi"` | Backing PersistentVolume storage size. |
| localModelNodeGroups[0].spec.persistentVolumeSpec.hostPath.path | string | `"/var/lib/kserve/localmodel"` | Host path used by the backing PersistentVolume. |
| localModelNodeGroups[0].spec.persistentVolumeSpec.persistentVolumeReclaimPolicy | string | `"Delete"` | Reclaim policy for the backing PersistentVolume. |
| localModelNodeGroups[0].spec.storageLimit | string | `"100Gi"` | Maximum aggregate storage allowed for the node group. |
| localModelNodes | list | `[{"annotations":{},"apiVersion":"serving.kserve.io/v1alpha1","enabled":false,"labels":{},"name":"example-localmodelnode","spec":{"localModels":[{"modelName":"example-model","nodeGroup":"example-node-group","sourceModelUri":"s3://models/example"}]},"status":{}}]` | LocalModelNode resources to render. |
| localModelNodes[0].enabled | bool | `false` | Set to `true` to render this resource. |
| localModelNodes[0].name | string | `"example-localmodelnode"` | Resource name. |
| localModelNodes[0].spec.localModels[0].modelName | string | `"example-model"` | Logical model name stored on the node. |
| localModelNodes[0].spec.localModels[0].nodeGroup | string | `"example-node-group"` | Target node group for this local model. |
| localModelNodes[0].spec.localModels[0].sourceModelUri | string | `"s3://models/example"` | Source model URI for this local model. |
| nameOverride | string | `""` | Override the default chart label name if needed. |
| servingRuntimes | list | `[{"annotations":{},"apiVersion":"serving.kserve.io/v1alpha1","enabled":false,"labels":{},"name":"example-servingruntime","namespace":"default","spec":{"containers":[{"args":["--model_name={{.Name}}","--model_dir=/mnt/models"],"image":"example/runtime:latest","name":"kserve-container"}],"supportedModelFormats":[{"autoSelect":true,"name":"sklearn","priority":1,"version":"1"}]},"status":{}}]` | ServingRuntime resources to render. |
| servingRuntimes[0].enabled | bool | `false` | Set to `true` to render this resource. |
| servingRuntimes[0].name | string | `"example-servingruntime"` | Resource name. |
| servingRuntimes[0].namespace | string | `"default"` | Resource namespace. Defaults to the Helm release namespace. |
| servingRuntimes[0].spec.containers[0].args | list | `["--model_name={{.Name}}","--model_dir=/mnt/models"]` | Runtime container arguments. |
| servingRuntimes[0].spec.containers[0].image | string | `"example/runtime:latest"` | Runtime container image. |
| servingRuntimes[0].spec.containers[0].name | string | `"kserve-container"` | Runtime container name. |
| servingRuntimes[0].spec.supportedModelFormats[0].autoSelect | bool | `true` | Mark this format for autoselection. |
| servingRuntimes[0].spec.supportedModelFormats[0].name | string | `"sklearn"` | Supported model format name. |
| servingRuntimes[0].spec.supportedModelFormats[0].priority | int | `1` | Priority used when multiple runtimes support the same format. |
| servingRuntimes[0].spec.supportedModelFormats[0].version | string | `"1"` | Supported model format version. |
| trainedModels | list | `[{"annotations":{},"apiVersion":"serving.kserve.io/v1alpha1","enabled":false,"labels":{},"name":"example-trainedmodel","namespace":"default","spec":{"inferenceService":"example-inferenceservice","model":{"framework":"sklearn","memory":"2Gi","storageUri":"s3://models/sklearn"}},"status":{}}]` | TrainedModel resources to render. |
| trainedModels[0].enabled | bool | `false` | Set to `true` to render this resource. |
| trainedModels[0].name | string | `"example-trainedmodel"` | Resource name. |
| trainedModels[0].namespace | string | `"default"` | Resource namespace. Defaults to the Helm release namespace. |
| trainedModels[0].spec.inferenceService | string | `"example-inferenceservice"` | Target InferenceService name. |
| trainedModels[0].spec.model.framework | string | `"sklearn"` | Model framework identifier. |
| trainedModels[0].spec.model.memory | string | `"2Gi"` | Memory request associated with the trained model. |
| trainedModels[0].spec.model.storageUri | string | `"s3://models/sklearn"` | Model storage URI. |

## Included Values Files

- [values.yaml](values.yaml): minimal defaults that render no resources.
- [values.yaml.example](values.yaml.example): example configuration covering every supported resource type.

## Testing

The repository uses three test layers:

- `tests/units/` for `helm-unittest` suites and backward compatibility checks
- `tests/e2e/` for local kind-based Helm install checks after bootstrapping KServe CRDs from vendored upstream manifests
- `tests/smokes/` for render and schema smoke scenarios

Representative local commands:

```bash
helm lint . -f values.yaml.example
helm template nuc-kserve . -f values.yaml.example
helm unittest -f 'tests/units/*_test.yaml' .
sh tests/units/backward_compatibility_test.sh
python3 tests/smokes/run/smoke.py --scenario example-render
make test-e2e
```
