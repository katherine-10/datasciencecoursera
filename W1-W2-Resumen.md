% Options for packages loaded elsewhere
\PassOptionsToPackage{unicode}{hyperref}
\PassOptionsToPackage{hyphens}{url}
%
\documentclass[
]{article}
\usepackage{lmodern}
\usepackage{amssymb,amsmath}
\usepackage{ifxetex,ifluatex}
\ifnum 0\ifxetex 1\fi\ifluatex 1\fi=0 % if pdftex
  \usepackage[T1]{fontenc}
  \usepackage[utf8]{inputenc}
  \usepackage{textcomp} % provide euro and other symbols
\else % if luatex or xetex
  \usepackage{unicode-math}
  \defaultfontfeatures{Scale=MatchLowercase}
  \defaultfontfeatures[\rmfamily]{Ligatures=TeX,Scale=1}
\fi
% Use upquote if available, for straight quotes in verbatim environments
\IfFileExists{upquote.sty}{\usepackage{upquote}}{}
\IfFileExists{microtype.sty}{% use microtype if available
  \usepackage[]{microtype}
  \UseMicrotypeSet[protrusion]{basicmath} % disable protrusion for tt fonts
}{}
\makeatletter
\@ifundefined{KOMAClassName}{% if non-KOMA class
  \IfFileExists{parskip.sty}{%
    \usepackage{parskip}
  }{% else
    \setlength{\parindent}{0pt}
    \setlength{\parskip}{6pt plus 2pt minus 1pt}}
}{% if KOMA class
  \KOMAoptions{parskip=half}}
\makeatother
\usepackage{xcolor}
\IfFileExists{xurl.sty}{\usepackage{xurl}}{} % add URL line breaks if available
\IfFileExists{bookmark.sty}{\usepackage{bookmark}}{\usepackage{hyperref}}
\hypersetup{
  pdftitle={Apuntes W1-W2},
  pdfauthor={katherine},
  hidelinks,
  pdfcreator={LaTeX via pandoc}}
\urlstyle{same} % disable monospaced font for URLs
\usepackage[margin=1in]{geometry}
\usepackage{graphicx,grffile}
\makeatletter
\def\maxwidth{\ifdim\Gin@nat@width>\linewidth\linewidth\else\Gin@nat@width\fi}
\def\maxheight{\ifdim\Gin@nat@height>\textheight\textheight\else\Gin@nat@height\fi}
\makeatother
% Scale images if necessary, so that they will not overflow the page
% margins by default, and it is still possible to overwrite the defaults
% using explicit options in \includegraphics[width, height, ...]{}
\setkeys{Gin}{width=\maxwidth,height=\maxheight,keepaspectratio}
% Set default figure placement to htbp
\makeatletter
\def\fps@figure{htbp}
\makeatother
\setlength{\emergencystretch}{3em} % prevent overfull lines
\providecommand{\tightlist}{%
  \setlength{\itemsep}{0pt}\setlength{\parskip}{0pt}}
\setcounter{secnumdepth}{-\maxdimen} % remove section numbering

\title{Apuntes W1-W2}
\author{katherine}
\date{4/7/2020}

\begin{document}
\maketitle

\hypertarget{apunte-y-resumen-de-funciones-de-semana-1-y-2-r-programming}{%
\subsection{Apunte y resumen de funciones de Semana 1 y 2 (R
Programming)}\label{apunte-y-resumen-de-funciones-de-semana-1-y-2-r-programming}}

Aspectos importantes: 1. Para crear vectores --\textgreater{} concatenar
2. Para asignar valores ``\textless-'' 3. Para acceder a la posición de
una lista {[}{[}{]}{]} 4. Para los índices podemos hacer secuencias o
indicar un arreglo de vectores

\begin{verbatim}

#1
c(1,2,3)
#2
x<-1:20 #Con los dos puntos no se utiliza la c :)
#3
x[1] #Aquí a diferencia de python los índices empiezan desde 1
#4
for i in seq_len(x) #Hago una secuencia del largo del arrego y recorro
for i in 1:20 # Recorro la secuencia directamente
\end{verbatim}

\hypertarget{para-matrices}{%
\subsection{Para Matrices}\label{para-matrices}}

\begin{enumerate}
\def\labelenumi{\arabic{enumi}.}
\tightlist
\item
  Creación de matrices
\item
  Attributes(matriz)--\textgreater{} me da las dimensiones de la matriz
\item
  Convertir un arreglo en matriz
\item
  Convertir dos arreglos en matriz
\end{enumerate}

\begin{verbatim}

#1 
m<-matrix(nrow=3,ncol = 2)
#2
attributes(m)
#3
x<-1:30 #Se declara un vector
dim(x)<-c(2,5) #Se declaran las dimensiones para el vector, queda una matriz de 2x5
#4
y<-1:30
cbind(x,y) #Se colocan los dos como vectores verticales
rbind(x,y) #Se colocan como vectores horizontales
\end{verbatim}

\hypertarget{lectura-y-manejo-de-datos}{%
\subsection{Lectura y Manejo de Datos}\label{lectura-y-manejo-de-datos}}

\begin{enumerate}
\def\labelenumi{\arabic{enumi}.}
\tightlist
\item
  Concatenar strings
\item
  Lectura de datos
\item
  Data Frames
\item
  Remover NA
\item
  Obtener dirección
\item
  Casos completos
\end{enumerate}

\begin{verbatim}
#1
paste(string1,string2,":)",sep = " ") #Se "pegan" los strings y se separan con espacio 
#2
read.csv("nombre.csv")#Para leer el archivo
#3
data.frame(dondepongo,titulo=deQueLoLleno)
#4
na.omit(ARCHIVO) #omito los datos que contienen NA
(!is.na(monitor_data$sulfate))  #Obtener todo lo que no sea Nulo
#5
getwd()
#6
complete(archivo)
\end{verbatim}

\hypertarget{subsetting}{%
\subsection{Subsetting}\label{subsetting}}

Seleccionar varios datos con condiciones y restricciones dentro de una
lista, frame, vector.

\begin{verbatim}
subset(arreglo,condicion)
\end{verbatim}

\hypertarget{anuxe1lisis-quiz-w2.}{%
\subsection{Análisis Quiz W2.}\label{anuxe1lisis-quiz-w2.}}

Implementación de métodos conocidos y nuevos métodos

\begin{verbatim}
#Primer punto del Assignment
pollutantmean <- function(directory, pollutant, id = 1:332) { #Creación de la función.

  means <- c() #Se declara la media de los archivos como un vector
  
  for(monitor in id){ #se recorren los archivos
    path <- paste(getwd(), "/", sprintf("%03d", monitor), ".csv", sep = "") #se crea la dirección del archivo según el escritorio en el que esté (Se puede añadir string con el parámetro de directory)
    monitor_data <- read.csv(path) #se lee el archivo
    interested_data <- monitor_data[pollutant] #Nos ubicamos en la fila que nos interesa, ya sea el de sulfato o nitrato (este depende del parámetro pollutant)
    means <- c(means, interested_data[!is.na(interested_data)]) #Se halla la media de los datos de interés excluyendo los NAs y añadiendo los valores al arreglo de medias
  }
  
  mean(means) #Se saca la media del arreglo de medias 
}

#Segundo punto del Assignment
complete<-function(directory,id=1:332){ #Se crea la función
  results <- data.frame(id=numeric(0), nobs=numeric(0)) #Se crea un frame para id inicializado en 0 y uno para nobs igual
  for(monitor in id){ #Se recorren los 132 archivos
    path <- paste(getwd(),"/", sprintf("%03d", monitor), ".csv", sep = "") #Se crea la ruta igual que en el punto anterior
    monitor_data <- read.csv(path) #se lee el archivo
    interested_data <- monitor_data[(!is.na(monitor_data$sulfate)), ] #Se eligen los datos que no tengan NAs (DE SULFATO)
    interested_data <- interested_data[(!is.na(interested_data$nitrate)), ] #Igual que el anterior pero para nitrato
    nobs <- nrow(interested_data) #asigno lel resultado de los dos filtros al numero de filas que tendrá nobs
    results <- rbind(results, data.frame(id=monitor, nobs=nobs))#el frame principal pongo los vectores horizontales y al id le asigno el valor del índice y el valor de nobs.
  }
  results #Retorno la tabla con los índices y los Nobs
}

#Tercer punto del Assignment
corr <- function(directory, threshold = 0){

  cor_results <- numeric(0) #inicializo en 0
  
  complete_cases <- complete(directory) #Solo elijo los que cumplan con todas las condiciones
  complete_cases <- complete_cases[complete_cases$nobs>=threshold, ] #Elijo de los casos completos los nobs que están sobre el lumbral

  
  if(nrow(complete_cases)>0){ #si hay filas
    for(monitor in complete_cases$id){ #recorro el id de los casos completos
      path <- paste(getwd(), "/", directory, "/", sprintf("%03d", monitor), ".csv", sep = "") #saco la direccipon, ubicación del archivo
      monitor_data <- read.csv(path) #leo el archivo
      interested_data <- monitor_data[(!is.na(monitor_data$sulfate)), ] #elijo todos los datos de sulfato que no tienen NAs
      interested_data <- interested_data[(!is.na(interested_data$nitrate)), ] #Filtro de nuevo para nitrato
      sulfate_data <- interested_data["sulfate"] #después del filtro saco los datos de sulfato
      nitrate_data <- interested_data["nitrate"]#después del filtro saco los datos de nitrato
      cor_results <- c(cor_results, cor(sulfate_data, nitrate_data)) #al arreglo añado la correlación de ambos datos
    }
  }
  cor_results #retorno el arreglo de las correlaciones de los datos
}
\end{verbatim}

\end{document}
