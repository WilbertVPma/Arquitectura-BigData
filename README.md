# Brainstorm

    Aplicaciones de Big Data en e-commerce.
    
----------------------------------------------------------------------------------------------------------------------------------------     
               
# **Diseño del DAaaS**

## Definición la estrategia del DAaaS:

###  a) Servicios:
  
               -Mejorar el nivel de venta de los productos con menos registros de compra.
               
               -Mejorar el catálogo de productos, conociendo las preferencias de la clientela.
               
               -Crear un sistema de precios dinámico basado en el mercado actual.
               
               -Definir estrategias de fidelización de la clientela.
  
###  b) Información requerida:
  
  	       1.Copia de la base de datos del catálogo de productos.
  	       
  	       2.Copia de la base de datos de clientes.
  	       
  	       3.Copia de la base registros de ventas.
  	       
  	       4.Copia de la base de datos de productos ofrecido por proveedores.
  	       
  	       5.Datasets de productos nuevos relacionados con el rubro de la empresa.
  	       
  	       6.Datasets del catálogo de productos y precios de otros e-commerce del mismo rubro.
  	       
  	       7.Registros de navegación en la web de ventas, en cuanto a tiempo de navegación y clicks de los clientes.
  	       
 ### c) Procesamiento de la información:
  
    	       -Del sistema del backup de la base de datos de la empresa, se enviará una copia a un bucket de Google Cloud Storage de 
    	        GCP exclusivamente para guardar los datos en crudo de la base de datos de la empresa.
    	        Esto se hará de forma periódica y automática mediante un cronjob y un script de Python utilizando Gsutil.
    	        En este paso se tendrán los datos en crudo del catálogo de productos, datos de clientes, datos de registro de ventas,
    	        y datos de productos ofrecidos por proveedores actuales de la empresa.
    	        Si este último no existe, se creará por parte de la empresa.
    	        
    	       -Se creará un proceso de scraping para tener datasets de productos nuevos relacionados al rubro de la empresa.
    	        Este proceso lo realizará alguna persona del departamento de ventas o similar, manualmente. También se enviará
    	        manualmente a un bucket de Google Cloud Storage exclusivamente para guardar los datos en crudo del scraping.
    	        
    	       -Se creará un proceso de scraping para tener datasets del catálogo de productos y precios de otros e-commerce del mismo 
    	        rubro.
    	        Este proceso lo realizará alguna persona del departamento de ventas o similar, manualmente. También se enviará
    	        manualmente a un bucket del Google Cloud Storage exclusivamente para guardar los datos en crudo del scraping.
    	        
    	       -Se crearán los registros de navegación de los clientes en la web de compras utilizando Google Analytic, y los resultados serán
		          enviados a un bucket en Google Cloud Storage.
    	       
  ### d) Limpieza y transformación de datos:
  
               -Teniendo los datos necesarios en crudo, serán limpiados y transformados por un ingeniero de datos o científico de datos.
               
               -Dependiendo de la empresa, hay posibilidades de automatizar los procesos de limpieza y transformación de los
                datos en crudo con Google Dataprep o Google Dataflow.
                
---------------------------------------------------------------------------------------------------------------------------------------- 
                
# **Diseño de la arquitectura**

## Definición de la estrategia del DAaaS:

###  a) Selección de componentes:
  
  	           1. Bases de datos de la empresa
  
	           2. Beautifulsoup
	       
	           3. Google Colab
  
               4. Google Cloud Platform:
               
                  4.1 GSutil
                  4.2 Google Cloud Storage
                  4.3 Google Cloud Analytics
                  4.4 Google Dataprep
                  4.5 Google Cloud Vertex AI
                  4.6 Google Cloud Functions
                  
               5. Tableau
                  

 ### b) Definición de procesos de ingeniería: 
  
               1. Conocer las características la empresa para entender la forma en que opera en el rubro en el que trabaja,
                  el tipo de infraestructura tecnológica con la cuenta y la forma en que las bases de datos está definida,
                  y si cuenta con la información necesaria para suplir las operaciones de IA.
               
               2. Definir con la empresa, el equipo donde se instalará GSutil para el envío automático de las copias de las
                  bases de datos a Google Cloud Platform.
                  
               3. Definir con la empresa, el equipo donde se harán los procesos de scraping para obtener los datasets de productos
                  nuevos y los datasets de productos y precios de empresas competencia. Ese mismo equipo tendrá acceso al
                  Google Cloud Storage para cargar manualmente los datasets obtenidos del scraping.
                  
               4. Creación de los script de scraping con las librerías de Beautifulsoup de Python, en Google Colab.
                  
               5. Creación del proyecto en Google Cloud Platform:
                  
                  5.1 Creación de cada uno de los buckets requeridos.
                  5.2 Configurar Google Analytics para obtener registros de conducta de los clientes en la web de compras,
                  5.3 Configurar el enlace Google Analytics y Google Cloud Storage.
                  5.4 Proceder a la limpieza de los datos en crudo alojados en las instancias en la nube.
                      Dependiendo de requerimientos de la empresa, el proceso de limpieza se puede hacer con Google Dataprep.
                  5.5 Diseñar los algoritmos de IA para responder a las necesidades predeterminadas por la empresa.
                  5.6 Configurar los algoritmos de IA para procesar los datasets previamente limpiados utilizando Vertex AI.
                  5.7 Configurar Vertex AI para que los resultados de los algoritmos sean enviados
                      al bucket de Google Cloud Storage predefinido con un script en Google Cloud Functions.
                      
               6. Instalación y configuración del software Tableau en un equipo determinado por la empresa.
                  
 ### c) Diseño de interfaces de usuario:
  
  	       1. Copia de base de datos del cliente a la nube: Estará en el equipo instalado con GSutil y un manual
  	       							de funcionamiento del software.
  	       
  	       2. Procesos de scraping: Estará dado por un notebook en Google Colab, que contará con los scripts de scraping con
  	       				con Beautifulsoup y un manual de funcionamiento.
  	       				
  	       3. Acceso al Google Cloud Storage: Se dará acceso a las instancias de los buckets en Google Cloud Storage.
  	       
  	       4. Visualización de dashboards con los resultados de los algoritmos de IA.
  	       				
  	       
###  d) Diseño y ejecución de Proofs-of-Concept:
  
  	       1. Creación del proyecto de la empresa en Google Cloud Platform.
  	       
  	       2. Creación de los buckets predeterminados en Google Cloud Storage.
  	       
  	       3. Instalación y configuración de GSutil en el equipo escogido para enviar los datasets a la nube.
  	       
  	       4. Cargar con un dataset de prueba en el equipo con GSutil para que sea enviado a la nube.
  	  
----------------------------------------------------------------------------------------------------------------------------------------  	       
  	       
# **DAaaS Operating Model Design and Rollout**

	       1. Creación de copia de base de datos de la empresa y su envío a la nube (who/when) GSutil / Cada mes.
	       
	       2. Ejecución de scripts de scraping a web seleccionadas y envío de resultados a la nube (who/when) Un empleado / Cada mes.
	       
	       3. Recopilación de datos de navegación de los clientes en la web de compras con Google Analytics, que mandará los datos
	          a Google Cloud Storage.
	          
	       4. Procesamiento de los datasets almacenados en Google Cloud Storage en Vertex AI.
	       
	       5. Exportar los resultados obtenidos en Vertex AI a un bucket de Google Cloud Storage 
	          (who/when) Google Cloud Functions / Cuando Vertex AI obtenga resultados.
	          
	       6. Descarga de los resutados en el bucket predeterminado para almacenar los resultados de los algoritmos de IA
	          (who/when) Un empleado / Cuando se requiera.
	       
	       7. Preparación de los dashboards con la información de los resultados de la IA utilizando Tableau.
	       
	       8. Establecimiento de comunicación con la empresa para consultas del rendimiento del sistema de la arquitectura Big Data
	          y resultados de los algoritmos de IA.
