# Convenciones de archivos
En este MD se detalla como se debe de llamar a los archivos\estructurar un proyecto etc..

## Naming de archivos
- tipo: PascalCase, ejemplos:
```
Core.mqh
Main.mqh
```
Esto solo para archivos como tal de codigo MQL5, en caso se requiera por ejemplo si se combina web\py se podrian aceptar los tipos de namig del otro ecosistema

## Estructura de proyecto de lib
Para los proyectos que sean modulos\libreries, se recomienda la siguiente estructuracion:
```
RepoName/
├── # Nota: Aqui pueden haber folders para workflows, etc....
├── Src/           # Codigo como tal del repo
├── Validation/    # Carpeta para los test finales del repo (para el CI)
└── Images/        # Imagenes que se usaran en la wiki\mds\banner del repo
```

## Estructura para EAs (No ai)
Para los proyectos que sean modulos\libreries, se recomienda la siguiente estructuracion:
```
RepoName/
├── # Nota: Aqui pueden haber folders para workflows, etc....
├── Core/          # Main + Defines + EAName + Global + (Functions si aplica)
├── Validation/    # Carpeta para los test finales del EA (para el CI)
├── Resrc/         # Recursos embebidos (opcional solo si aplica)
└── Images/        # Imagenes que se usaran en la wiki\mds\banner del repo
```

## Estrucutura para EAs que implementen IA (Convencion de AiDataGenByLeo)
Para los proyectos que sean modulos\libreries, se recomienda la siguiente estructuracion:
```
RepoName/
├── # Nota: Aqui pueden haber folders para workflows, etc....
├──  AiAd/         # Folder para clases de prediccion
├── Models/        # Integracion de modelos ONNX especificos
├── Core/          # Main + Defines + EAName + Global + (Functions si aplica)
├── Resrc/         # Recursos embebidos del ea
├── Validation/    # Carpeta para los test finales del EA (para el CI)
└── Images/        # Imagenes que se usaran en la wiki\mds\banner del repo
```



