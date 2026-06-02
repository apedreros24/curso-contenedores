# Laboratorio 3 - CI/CD con Jenkins y Kubernetes

## Alumna

Arlette Pedreros

## Descripción

Implementación de una aplicación NestJS desplegada mediante un pipeline CI/CD utilizando Jenkins, Docker y Kubernetes.

## Requisitos

* Docker Desktop con Kubernetes habilitado
* kubectl
* Jenkins
* Git
* Node.js y pnpm

## Estructura del proyecto

* Dockerfile
* Jenkinsfile
* agent.yaml
* entrega.yaml
* src/
* test/
* evidencias/

## Imagen Docker

Repositorio:

apedreros24/tarea-final

Tag:

arlette-pedreros

## Despliegue manual

### Construir imagen

```bash
docker build -t apedreros24/tarea-final:arlette-pedreros .
```

### Ejecutar contenedor localmente

```bash
docker run --rm -p 3000:3000 \
-e AMBIENTE=docker \
-e API_KEY=api-docker \
apedreros24/tarea-final:arlette-pedreros
```

### Aplicar recursos Kubernetes

```bash
kubectl apply -f entrega.yaml
```

### Verificar recursos

```bash
kubectl get pods -n ns-arlette-pedreros
kubectl get deployment -n ns-arlette-pedreros
kubectl get svc -n ns-arlette-pedreros
```

### Acceder a la aplicación

```bash
kubectl port-forward svc/svc-arlette-pedreros 8080:80 -n ns-arlette-pedreros
```

En otra terminal:

```bash
curl http://localhost:8080/lab
```

Resultado esperado:

```json
{"AMBIENTE":"kubernetes","API_KEY":"api-key-arlette"}
```

## Pipeline Jenkins

El pipeline ejecuta las siguientes etapas:

* install
* test
* build
* push
* deploy

## Evidencias

Las evidencias del laboratorio se encuentran en la carpeta:

evidencias/

Incluyen:

* Ejecución exitosa de Jenkins
* Pods en estado Running
* Deployment
* Service
* ConfigMap
* Secret
* Docker Hub
* Validación de la aplicación
