aqui poner todos mis datos
# Curso Postgres Avanzado

# autora: Devorath Samanta Barrios Garcia

## Nombre del proyecto: Monitoreo

#### El proyecto se plantea por la necesidad de comunicaciones internas seguras, la base debe permitir recabar la información de documentos, mensajes, mensajes grupales, audios, ubicaciones, cooordenadas, fecha, hora, para esta acciones, además de contar con las caracterísitcas funcionales como las que actualmente ofrecen WhatsApp, Telegram. Se ajunta archivo excel con datos generales y en consideración del tipo de información que se encuentra clasificada como confidencial por contener datos personales. Se realiza un análisis de la informacion para definir las tablas y catálogos para el usuario y el login.

[Descarga el archivo concentrado para mayor referencia]
(https://github.com/Devorath/Postgres/blob/20ac9ffd904940fcc86fc53cbdfb089646df6790/1.%20Obtenci%C3%B3n%20de%20datos/concentrado.xls)

##### Configuración del entorno SQL

##### Interfaz gráfica de postgres, del lado izquierdo se encuentran los servers activos, las bases de datos, los Casts, Schemas,las tablas, índices, vistas, etc. Login/usuarios/roles. También se puede acceder al Shell, en el caso del Shell viene por default y está listo para ser utilizado y en el cmd de windows C:/Program Files/PostgreSQL/14/bin/.

[Consulta las imagenes para mayor referencia]
(https://github.com/Devorath/Postgres/tree/main/2.%20Configuraci%C3%B3n%20del%20entorno%20SQL)

### Diseño de la base de datos, el modelado de la base de datos se realiza mediante un modelado diagrama ER_Monitoreo.
### Crearemos una base de datos como db_monitoreo, un schema monitoreo y las tablas que permitan registrar a un usuario, y 
##  almacenar ese usuario y una contraseña. Las tablas consideradas son 2 y 4 catálogos, como a continuación se detalla:
 
###  tbl_user, registra los datos personales.
###  tbl_login, registra el password de los usuarios.
###  cat_position_grade es un catálogo de cargos y grados.
###  cat_gral_coord almacena el catálogo 
###  cat_coordination, almacena la coordinación estatal.
###  cat_battalion almacena el catálogo de batallón.

### Tipos de datos que se usarán en la cración de las tablas:
### PRIMARY KEY, Constraint, Not Null, chacter varying(50), integer.

```sql
-- This script was generated by the ERD tool in pgAdmin 4.
-- Please log an issue at https://github.com/pgadmin-org/pgadmin4/issues/new/choose if you find any bugs, including reproduction steps.

--
-- PostgreSQL database dump
--

-- Dumped from database version 15.2
-- Dumped by pg_dump version 15.2

-- Started on 2024-06-27 16:55:16

SET statement_timeout = 0;
SET lock_timeout = 0;
SET idle_in_transaction_session_timeout = 0;
SET client_encoding = 'UTF8';
SET standard_conforming_strings = on;
SELECT pg_catalog.set_config('search_path', '', false);
SET check_function_bodies = false;
SET xmloption = content;
SET client_min_messages = warning;
SET row_security = off;

--
-- TOC entry 5 (class 2615 OID 16882)
-- Name: monitoreo; Type: SCHEMA; Schema: -; Owner: postgres
--

CREATE SCHEMA monitoreo;


ALTER SCHEMA monitoreo OWNER TO postgres;

SET default_tablespace = '';

SET default_table_access_method = heap;

--
-- TOC entry 221 (class 1259 OID 25081)
-- Name: cat_battalion; Type: TABLE; Schema: monitoreo; Owner: postgres
--

CREATE TABLE monitoreo.cat_battalion (
    id_battalion integer NOT NULL,
    battalion character varying(50) NOT NULL
);


ALTER TABLE monitoreo.cat_battalion OWNER TO postgres;

--
-- TOC entry 220 (class 1259 OID 25080)
-- Name: cat_battalion_id_battalion_seq; Type: SEQUENCE; Schema: monitoreo; Owner: postgres
--

CREATE SEQUENCE monitoreo.cat_battalion_id_battalion_seq
    AS integer
    START WITH 1
    INCREMENT BY 1
    NO MINVALUE
    NO MAXVALUE
    CACHE 1;


ALTER TABLE monitoreo.cat_battalion_id_battalion_seq OWNER TO postgres;

--
-- TOC entry 3382 (class 0 OID 0)
-- Dependencies: 220
-- Name: cat_battalion_id_battalion_seq; Type: SEQUENCE OWNED BY; Schema: monitoreo; Owner: postgres
--

ALTER SEQUENCE monitoreo.cat_battalion_id_battalion_seq OWNED BY monitoreo.cat_battalion.id_battalion;


--
-- TOC entry 223 (class 1259 OID 25088)
-- Name: cat_coordination; Type: TABLE; Schema: monitoreo; Owner: postgres
--

CREATE TABLE monitoreo.cat_coordination (
    id_coordination integer NOT NULL,
    coordination character varying NOT NULL
);


ALTER TABLE monitoreo.cat_coordination OWNER TO postgres;

--
-- TOC entry 222 (class 1259 OID 25087)
-- Name: cat_coordination_cat_coordination_seq; Type: SEQUENCE; Schema: monitoreo; Owner: postgres
--

CREATE SEQUENCE monitoreo.cat_coordination_cat_coordination_seq
    AS integer
    START WITH 1
    INCREMENT BY 1
    NO MINVALUE
    NO MAXVALUE
    CACHE 1;


ALTER TABLE monitoreo.cat_coordination_cat_coordination_seq OWNER TO postgres;

--
-- TOC entry 3383 (class 0 OID 0)
-- Dependencies: 222
-- Name: cat_coordination_cat_coordination_seq; Type: SEQUENCE OWNED BY; Schema: monitoreo; Owner: postgres
--

ALTER SEQUENCE monitoreo.cat_coordination_cat_coordination_seq OWNED BY monitoreo.cat_coordination.id_coordination;


--
-- TOC entry 219 (class 1259 OID 25074)
-- Name: cat_gral_coord; Type: TABLE; Schema: monitoreo; Owner: postgres
--

CREATE TABLE monitoreo.cat_gral_coord (
    id_gral_coord integer NOT NULL,
    gral_coord character varying NOT NULL
);


ALTER TABLE monitoreo.cat_gral_coord OWNER TO postgres;

--
-- TOC entry 218 (class 1259 OID 25073)
-- Name: cat_gral_coord_id_gral_coord_seq; Type: SEQUENCE; Schema: monitoreo; Owner: postgres
--

CREATE SEQUENCE monitoreo.cat_gral_coord_id_gral_coord_seq
    AS integer
    START WITH 1
    INCREMENT BY 1
    NO MINVALUE
    NO MAXVALUE
    CACHE 1;


ALTER TABLE monitoreo.cat_gral_coord_id_gral_coord_seq OWNER TO postgres;

--
-- TOC entry 3384 (class 0 OID 0)
-- Dependencies: 218
-- Name: cat_gral_coord_id_gral_coord_seq; Type: SEQUENCE OWNED BY; Schema: monitoreo; Owner: postgres
--

ALTER SEQUENCE monitoreo.cat_gral_coord_id_gral_coord_seq OWNED BY monitoreo.cat_gral_coord.id_gral_coord;


--
-- TOC entry 225 (class 1259 OID 25095)
-- Name: cat_position_grade; Type: TABLE; Schema: monitoreo; Owner: postgres
--

CREATE TABLE monitoreo.cat_position_grade (
    id_position_grade integer NOT NULL,
    position_grado character varying(50) NOT NULL
);


ALTER TABLE monitoreo.cat_position_grade OWNER TO postgres;

--
-- TOC entry 224 (class 1259 OID 25094)
-- Name: cat_position_grade_id_position_grade_seq; Type: SEQUENCE; Schema: monitoreo; Owner: postgres
--

CREATE SEQUENCE monitoreo.cat_position_grade_id_position_grade_seq
    AS integer
    START WITH 1
    INCREMENT BY 1
    NO MINVALUE
    NO MAXVALUE
    CACHE 1;


ALTER TABLE monitoreo.cat_position_grade_id_position_grade_seq OWNER TO postgres;

--
-- TOC entry 3385 (class 0 OID 0)
-- Dependencies: 224
-- Name: cat_position_grade_id_position_grade_seq; Type: SEQUENCE OWNED BY; Schema: monitoreo; Owner: postgres
--

ALTER SEQUENCE monitoreo.cat_position_grade_id_position_grade_seq OWNED BY monitoreo.cat_position_grade.id_position_grade;


--
-- TOC entry 217 (class 1259 OID 16930)
-- Name: tbl_login; Type: TABLE; Schema: monitoreo; Owner: postgres
--

CREATE TABLE monitoreo.tbl_login (
    id_login integer NOT NULL,
    user_name character varying(250) NOT NULL,
    password character varying(500) NOT NULL,
    id_user integer
);


ALTER TABLE monitoreo.tbl_login OWNER TO postgres;

--
-- TOC entry 216 (class 1259 OID 16927)
-- Name: tbl_login_id_login_seq; Type: SEQUENCE; Schema: monitoreo; Owner: postgres
--

CREATE SEQUENCE monitoreo.tbl_login_id_login_seq
    AS integer
    START WITH 1
    INCREMENT BY 1
    NO MINVALUE
    NO MAXVALUE
    CACHE 1;


ALTER TABLE monitoreo.tbl_login_id_login_seq OWNER TO postgres;

--
-- TOC entry 3386 (class 0 OID 0)
-- Dependencies: 216
-- Name: tbl_login_id_login_seq; Type: SEQUENCE OWNED BY; Schema: monitoreo; Owner: postgres
--

ALTER SEQUENCE monitoreo.tbl_login_id_login_seq OWNED BY monitoreo.tbl_login.id_login;


--
-- TOC entry 215 (class 1259 OID 16919)
-- Name: tbl_user; Type: TABLE; Schema: monitoreo; Owner: postgres
--

CREATE TABLE monitoreo.tbl_user (
    id_user integer NOT NULL,
    username character varying(50) NOT NULL,
    pat_name character varying(50) NOT NULL,
    mat_name character varying(50) NOT NULL,
    contact_num numeric NOT NULL,
    regis_num integer NOT NULL,
    id_battalion integer NOT NULL,
    id_coordination integer NOT NULL,
    id_gral_coord integer NOT NULL,
    id_position_grade integer NOT NULL
);


ALTER TABLE monitoreo.tbl_user OWNER TO postgres;

--
-- TOC entry 226 (class 1259 OID 25130)
-- Name: tbl_user_id_battalion_seq; Type: SEQUENCE; Schema: monitoreo; Owner: postgres
--

CREATE SEQUENCE monitoreo.tbl_user_id_battalion_seq
    AS integer
    START WITH 1
    INCREMENT BY 1
    NO MINVALUE
    NO MAXVALUE
    CACHE 1;


ALTER TABLE monitoreo.tbl_user_id_battalion_seq OWNER TO postgres;

--
-- TOC entry 3387 (class 0 OID 0)
-- Dependencies: 226
-- Name: tbl_user_id_battalion_seq; Type: SEQUENCE OWNED BY; Schema: monitoreo; Owner: postgres
--

ALTER SEQUENCE monitoreo.tbl_user_id_battalion_seq OWNED BY monitoreo.tbl_user.id_battalion;


--
-- TOC entry 214 (class 1259 OID 16918)
-- Name: tbl_user_id_user_seq; Type: SEQUENCE; Schema: monitoreo; Owner: postgres
--

CREATE SEQUENCE monitoreo.tbl_user_id_user_seq
    AS integer
    START WITH 1
    INCREMENT BY 1
    NO MINVALUE
    NO MAXVALUE
    CACHE 1;


ALTER TABLE monitoreo.tbl_user_id_user_seq OWNER TO postgres;

--
-- TOC entry 3388 (class 0 OID 0)
-- Dependencies: 214
-- Name: tbl_user_id_user_seq; Type: SEQUENCE OWNED BY; Schema: monitoreo; Owner: postgres
--

ALTER SEQUENCE monitoreo.tbl_user_id_user_seq OWNED BY monitoreo.tbl_user.id_user;


--
-- TOC entry 3200 (class 2604 OID 25084)
-- Name: cat_battalion id_battalion; Type: DEFAULT; Schema: monitoreo; Owner: postgres
--

ALTER TABLE ONLY monitoreo.cat_battalion ALTER COLUMN id_battalion SET DEFAULT nextval('monitoreo.cat_battalion_id_battalion_seq'::regclass);


--
-- TOC entry 3201 (class 2604 OID 25091)
-- Name: cat_coordination id_coordination; Type: DEFAULT; Schema: monitoreo; Owner: postgres
--

ALTER TABLE ONLY monitoreo.cat_coordination ALTER COLUMN id_coordination SET DEFAULT nextval('monitoreo.cat_coordination_cat_coordination_seq'::regclass);


--
-- TOC entry 3199 (class 2604 OID 25077)
-- Name: cat_gral_coord id_gral_coord; Type: DEFAULT; Schema: monitoreo; Owner: postgres
--

ALTER TABLE ONLY monitoreo.cat_gral_coord ALTER COLUMN id_gral_coord SET DEFAULT nextval('monitoreo.cat_gral_coord_id_gral_coord_seq'::regclass);


--
-- TOC entry 3202 (class 2604 OID 25098)
-- Name: cat_position_grade id_position_grade; Type: DEFAULT; Schema: monitoreo; Owner: postgres
--

ALTER TABLE ONLY monitoreo.cat_position_grade ALTER COLUMN id_position_grade SET DEFAULT nextval('monitoreo.cat_position_grade_id_position_grade_seq'::regclass);


--
-- TOC entry 3371 (class 0 OID 25081)
-- Dependencies: 221
-- Data for Name: cat_battalion; Type: TABLE DATA; Schema: monitoreo; Owner: postgres
--

COPY monitoreo.cat_battalion (id_battalion, battalion) FROM stdin;
0	S/D
1	Celaya
2	Aguascalientes
3	Jalpa de Serra
4	Guadalupe
5	San Luis de la Paz
6	Río Grande 
7	Acambaro
8	Colima
9	Santiago Ixcuintla
10	Tepic
\.


--
-- TOC entry 3373 (class 0 OID 25088)
-- Dependencies: 223
-- Data for Name: cat_coordination; Type: TABLE DATA; Schema: monitoreo; Owner: postgres
--

COPY monitoreo.cat_coordination (id_coordination, coordination) FROM stdin;
1	Coordinación Estatal de la Guardia Nacional Aguascalientes
2	Coordinación Estatal de la Guardia Nacional Chihuahua
3	Coordinación Estatal de la Guardia Nacional Campeche
4	Coordinación Estatal de la Guardia Nacional Sonora
5	Coordinación Estatal de la Guardia Nacional Colima
6	Coordinación Estatal de la Guardia Nacional Nuevo León
7	Coordinación Estatal de la Guardia Nacional Zacatecas
8	Coordinación Estatal de la Guardia Nacional  Baja California
9	Coordinación Estatal de la Guardia Nacional Querétaro 
10	Coordinación Estatal de la Guardia Nacional Oaxaca
11	Coordinación Estatal de la Guardia Nacional Nayarit
0	S/D
12	Coordinación Estatal de la Guardia Nacional Guanajuato
13	Coordinación Estatal de la Guardia Nacional Zacatecas
14	Otro
\.


--
-- TOC entry 3369 (class 0 OID 25074)
-- Dependencies: 219
-- Data for Name: cat_gral_coord; Type: TABLE DATA; Schema: monitoreo; Owner: postgres
--

COPY monitoreo.cat_gral_coord (id_gral_coord, gral_coord) FROM stdin;
1	Dirección General Antidrogas
2	Dirección General de Inteligencia
3	Dirección General de Investigación
4	Dirección General de Tecnologías de la Información y Comunicación
5	Unidad Especializada de Órganos por Competencia
6	Unidad de Asuntos Jurídicos y Transparencia de la Guardia Nacional
7	Unidad de Asuntos Internos
8	Dirección General de Administración y Finanzas
0	S/D
9	Otro
\.


--
-- TOC entry 3375 (class 0 OID 25095)
-- Dependencies: 225
-- Data for Name: cat_position_grade; Type: TABLE DATA; Schema: monitoreo; Owner: postgres
--

COPY monitoreo.cat_position_grade (id_position_grade, position_grado) FROM stdin;
1	Director de Área
2	Subdirector(a)
3	Jefe de departamento
4	Guardia
5	Subagente
6	Agente
7	Agente Mayor
8	Suboficial
9	Oficial
10	Segundo Subinspector
11	Primer Subinsoector
12	Inspector Jefe
13	Inspector General
14	Analista
\.


--
-- TOC entry 3367 (class 0 OID 16930)
-- Dependencies: 217
-- Data for Name: tbl_login; Type: TABLE DATA; Schema: monitoreo; Owner: postgres
--

COPY monitoreo.tbl_login (id_login, user_name, password, id_user) FROM stdin;
2	RomanJ_12	jkjnkjnm,246531265465xzcdcfadfcad53132c1d1v323fv	\N
1	omar_1	kmlkmlklmkmkmlml5612331652132131321sdafedcdfvvfvfd3f21v231c3	\N
\.


--
-- TOC entry 3365 (class 0 OID 16919)
-- Dependencies: 215
-- Data for Name: tbl_user; Type: TABLE DATA; Schema: monitoreo; Owner: postgres
--

COPY monitoreo.tbl_user (id_user, username, pat_name, mat_name, contact_num, regis_num, id_battalion, id_coordination, id_gral_coord, id_position_grade) FROM stdin;
2	EDGAR JULIO	ESPINOZA	PALOMARES	5269284912	61037	2	1	8	4
3	FRANCISCO JAVIER	ROJAS	AGUILAR	2628491355	64655	1	12	3	6
4	MAYRA	HERNANDEZ	SANCHEZ	6284981624	62230	2	1	5	1
5	 ALBERTO	BAHENA	RIOS	7221682900	65007	1	12	1	5
6	LUIS SERGIO	BERRU	MAYO	9821682901	64842	1	12	7	7
7	DANIEL HECTOR	CASTILLO	RAYON	8975642533	64711	1	12	4	7
8	RICARDO	CAMACHO	CONTRERAS	9814562315	64887	1	12	2	7
9	ARIAN	MEJIA	AUSTRIA	5556114600	64685	1	12	2	2
10	CRISTOFER	ENCARNACION	IBARRA	244987623	63096	3	9	1	4
11	RICARDO ANGEL	GUTIERREZ	GALLO	798456110	64724	4	13	7	13
12	HUGO ABRAHAM	CABILDO	AGUIRRE	564789256	63795	1	12	7	8
13	PEDRO ADALFONSO	GONZALEZ	PINEDA	5689754612	64764	1	12	4	8
14	CARLOS ALBERTO	LOPEZ	PEREZ	5526284924	64521	3	9	2	8
15	VICTOR	RIVERA	GARCIA	5561849732	64616	3	9	3	13
16	OSCAR	NAVARRO	GUTIERREZ	2467891496	63851	1	12	8	3
17	MIRIAM	MEDINA	LIMA	981478936	64771	1	12	2	6
18	JOSE DANIEL	MARTINEZ	SANTOS	654924530	64861	1	12	5	7
19	DANIEL	TORRES	BARRIENTOS	857623321	64877	1	12	7	1
20	NILO	SANTOS	MORENO	5578945612	64918	2	1	4	1
21	EDGAR ERNESTO	JIMENEZ	SOSA	569875612	64982	5	12	7	1
22	ADILENE	CRUZ	SOLIS	530156525	65126	1	12	1	8
23	EDILBERTO	AVELINO	ROBLES	269587140	64816	1	12	8	3
24	WILLIAM	CANTE	SOLIS	530189745	64967	5	12	2	6
25	GOVANNI	SANCHEZ	SANCHEZ	2197863545	64571	6	13	5	8
26	OSCAR SANTIAGO	MANRIQUEZ	SORIA	3337894569	62346	2	1	7	5
27	ANTONIO	JACINTO	REYES	4562359879	64768	3	9	8	4
28	FABIAN	RODRIGUEZ	ROJAS	445589750	65193	5	12	2	4
29	HUMBERTO ESTEBAN	SANCHEZ	RAMIREZ	4563226858	63857	7	12	4	3
30	AUREO	SILVA	VENTURA	4562398762	64776	2	1	2	9
31	CARLOS	MENDOZA	SANTOS	5578954600	64864	1	12	6	8
32	FIDEL	MENDOZA	MEJIA	5894254555	65144	2	1	2	11
33	JAIME	GARRIDO	VIVEROS	2198746205	64788	8	5	2	14
34	YONIC FRANCISCO	SANCHEZ	SANCHEZ	6894521088	63473	8	5	1	11
35	JUAN	LEAL	GARCIA	7982310455	64726	8	5	2	13
36	EUSTACIO	CORDOVA	RODRIGUEZ	4568976458	64924	8	5	6	5
37	DARIO	TREJO	VALDEZ	5689702550	64704	8	5	7	6
38	FLORENCIO	SERAPIO	BARRIOS	56897622	65033	8	12	3	13
39	ERNESTO	ALBA	LOVERA	45589761524	64665	2	1	7	13
40	SERGIO	DURAN	MORENO	58974560563	64786	1	12	2	14
41	JOSE MARGARITO	CARMONA	RAMIREZ	5789200322	64782	1	12	2	9
42	PEDRO ANTONIO	VARGAS	GARCIA	7448945600	64921	9	11	3	2
43	FRANCISCO	RIOS	RUIZ	1456789234	65189	10	11	8	14
44	ALEJANDRO GERMAN	AGUILAR	HERNANDEZ	567892022	65121	1	12	3	3
45	ARMANDO DAVID	TEXPAN	GARCIA	8974560987	63860	2	1	7	2
46	GABRIEL	RUIZ	MORALES	5689756941	64998	1	12	6	3
47	DIANA BERENICE	NAJERA	BRAVO	7895623785	65106	1	12	1	9
48	JESUS ANGEL	SANCHEZ	GUTIERREZ	7772456897	64659	3	9	5	8
49	JOSE ANTONIO	BERMUDEZ	HERNANDEZ	7738945612	65080	8	5	4	6
50	ARMANDO	SALAS	GOMEZ	7845995687	64657	3	9	5	14
51	LETICIA	HERNANDEZ	MAXIMO	5301565255	65052	1	12	8	3
1	RUBEN OMAR\n	JARAMILLO	MARISCAL	5526284911	50314	1	12	1	11
\.


--
-- TOC entry 3389 (class 0 OID 0)
-- Dependencies: 220
-- Name: cat_battalion_id_battalion_seq; Type: SEQUENCE SET; Schema: monitoreo; Owner: postgres
--

SELECT pg_catalog.setval('monitoreo.cat_battalion_id_battalion_seq', 2, true);


--
-- TOC entry 3390 (class 0 OID 0)
-- Dependencies: 222
-- Name: cat_coordination_cat_coordination_seq; Type: SEQUENCE SET; Schema: monitoreo; Owner: postgres
--

SELECT pg_catalog.setval('monitoreo.cat_coordination_cat_coordination_seq', 11, true);


--
-- TOC entry 3391 (class 0 OID 0)
-- Dependencies: 218
-- Name: cat_gral_coord_id_gral_coord_seq; Type: SEQUENCE SET; Schema: monitoreo; Owner: postgres
--

SELECT pg_catalog.setval('monitoreo.cat_gral_coord_id_gral_coord_seq', 12, true);


--
-- TOC entry 3392 (class 0 OID 0)
-- Dependencies: 224
-- Name: cat_position_grade_id_position_grade_seq; Type: SEQUENCE SET; Schema: monitoreo; Owner: postgres
--

SELECT pg_catalog.setval('monitoreo.cat_position_grade_id_position_grade_seq', 16, true);


--
-- TOC entry 3393 (class 0 OID 0)
-- Dependencies: 216
-- Name: tbl_login_id_login_seq; Type: SEQUENCE SET; Schema: monitoreo; Owner: postgres
--

SELECT pg_catalog.setval('monitoreo.tbl_login_id_login_seq', 2, true);


--
-- TOC entry 3394 (class 0 OID 0)
-- Dependencies: 226
-- Name: tbl_user_id_battalion_seq; Type: SEQUENCE SET; Schema: monitoreo; Owner: postgres
--

SELECT pg_catalog.setval('monitoreo.tbl_user_id_battalion_seq', 1, false);


--
-- TOC entry 3395 (class 0 OID 0)
-- Dependencies: 214
-- Name: tbl_user_id_user_seq; Type: SEQUENCE SET; Schema: monitoreo; Owner: postgres
--

SELECT pg_catalog.setval('monitoreo.tbl_user_id_user_seq', 1, true);


--
-- TOC entry 3212 (class 2606 OID 25086)
-- Name: cat_battalion cat_battalion_pkey; Type: CONSTRAINT; Schema: monitoreo; Owner: postgres
--

ALTER TABLE ONLY monitoreo.cat_battalion
    ADD CONSTRAINT cat_battalion_pkey PRIMARY KEY (id_battalion);


--
-- TOC entry 3214 (class 2606 OID 25093)
-- Name: cat_coordination cat_coordination_pkey; Type: CONSTRAINT; Schema: monitoreo; Owner: postgres
--

ALTER TABLE ONLY monitoreo.cat_coordination
    ADD CONSTRAINT cat_coordination_pkey PRIMARY KEY (id_coordination);


--
-- TOC entry 3210 (class 2606 OID 25079)
-- Name: cat_gral_coord cat_gral_coord_pkey; Type: CONSTRAINT; Schema: monitoreo; Owner: postgres
--

ALTER TABLE ONLY monitoreo.cat_gral_coord
    ADD CONSTRAINT cat_gral_coord_pkey PRIMARY KEY (id_gral_coord);


--
-- TOC entry 3216 (class 2606 OID 25100)
-- Name: cat_position_grade cat_position_grade_pkey; Type: CONSTRAINT; Schema: monitoreo; Owner: postgres
--

ALTER TABLE ONLY monitoreo.cat_position_grade
    ADD CONSTRAINT cat_position_grade_pkey PRIMARY KEY (id_position_grade);


--
-- TOC entry 3208 (class 2606 OID 16937)
-- Name: tbl_login tbl_login_pkey; Type: CONSTRAINT; Schema: monitoreo; Owner: postgres
--

ALTER TABLE ONLY monitoreo.tbl_login
    ADD CONSTRAINT tbl_login_pkey PRIMARY KEY (id_login);


--
-- TOC entry 3204 (class 2606 OID 16924)
-- Name: tbl_user tbl_user_pkey; Type: CONSTRAINT; Schema: monitoreo; Owner: postgres
--

ALTER TABLE ONLY monitoreo.tbl_user
    ADD CONSTRAINT tbl_user_pkey PRIMARY KEY (id_user);


--
-- TOC entry 3206 (class 2606 OID 16926)
-- Name: tbl_user tbl_user_username_key; Type: CONSTRAINT; Schema: monitoreo; Owner: postgres
--

ALTER TABLE ONLY monitoreo.tbl_user
    ADD CONSTRAINT tbl_user_username_key UNIQUE (username);


--
-- TOC entry 3221 (class 2606 OID 25870)
-- Name: tbl_login tbl_login_id_user_fkey; Type: FK CONSTRAINT; Schema: monitoreo; Owner: postgres
--

ALTER TABLE ONLY monitoreo.tbl_login
    ADD CONSTRAINT tbl_login_id_user_fkey FOREIGN KEY (id_user) REFERENCES monitoreo.tbl_user(id_user) NOT VALID;


--
-- TOC entry 3217 (class 2606 OID 25147)
-- Name: tbl_user tbl_user_id_battalion_fkey; Type: FK CONSTRAINT; Schema: monitoreo; Owner: postgres
--

ALTER TABLE ONLY monitoreo.tbl_user
    ADD CONSTRAINT tbl_user_id_battalion_fkey FOREIGN KEY (id_battalion) REFERENCES monitoreo.cat_battalion(id_battalion) NOT VALID;


--
-- TOC entry 3218 (class 2606 OID 25223)
-- Name: tbl_user tbl_user_id_coordination_fkey; Type: FK CONSTRAINT; Schema: monitoreo; Owner: postgres
--

ALTER TABLE ONLY monitoreo.tbl_user
    ADD CONSTRAINT tbl_user_id_coordination_fkey FOREIGN KEY (id_coordination) REFERENCES monitoreo.cat_coordination(id_coordination) NOT VALID;


--
-- TOC entry 3219 (class 2606 OID 25233)
-- Name: tbl_user tbl_user_id_gral_coord_fkey; Type: FK CONSTRAINT; Schema: monitoreo; Owner: postgres
--

ALTER TABLE ONLY monitoreo.tbl_user
    ADD CONSTRAINT tbl_user_id_gral_coord_fkey FOREIGN KEY (id_gral_coord) REFERENCES monitoreo.cat_gral_coord(id_gral_coord) NOT VALID;


--
-- TOC entry 3220 (class 2606 OID 25238)
-- Name: tbl_user tbl_user_id_position_grade_fkey; Type: FK CONSTRAINT; Schema: monitoreo; Owner: postgres
--

ALTER TABLE ONLY monitoreo.tbl_user
    ADD CONSTRAINT tbl_user_id_position_grade_fkey FOREIGN KEY (id_position_grade) REFERENCES monitoreo.cat_position_grade(id_position_grade) NOT VALID;


-- Completed on 2024-06-27 16:55:16
--
-- PostgreSQL database dump complete
--
```

### Gestión de usuarios, Seguridad y Privilegios.

## Se genera un usuario con permisos para usuario(role), password(m0nit0r)
### ![alt text](image.png)

```sql
CREATE ROLE monitor WITH
	LOGIN
	NOSUPERUSER
	NOCREATEDB
	NOCREATEROLE
	INHERIT
	REPLICATION
	CONNECTION LIMIT -1;
```

### Creando una copia de seguridad


### Archivo de BACKUP de la base de datos.

[Descarga la copia de seguridad]
(https://github.com/Devorath/Postgres/tree/20ac9ffd904940fcc86fc53cbdfb089646df6790/5.%20Creando%20copia)

### Optimizando consultas mediante indice, 

CREATE INDEX idx_tbl_user_username ON monitoreo.tbl_user (username);

### Concatena el nombre, apellido paterno, apellido materno (puesto que el nombre, apellidos son necesarios para todas las consultas)

```sql
SELECT id_user,
	concat(username, ' ', pat_name, ' ', mat_name) AS nombre_completo
FROM monitoreo."tbl_user";
```
### Genera una consulta que muestre de la tabla id_user el nombre completo del usuario y el id_cat_battalion sea = 3 (esto puede ser de gran utilidad cuando se consulte por registros especificos de un catálogo)

```sql
SELECT a.id_user, e.id_battalion,
    CONCAT(a.username, ' ', a.pat_name, ' ', a.mat_name) AS nombre_completo
FROM monitoreo."tbl_user" AS a 
JOIN monitoreo."cat_battalion" AS e
    ON a.id_battalion = e.id_battalion
WHERE e.id_battalion = 3
ORDER BY a.id_user;
```
### Genera una consulta que muestre de la tabla id_user el nombre completo del usuario, el battalion sea = 'Celaya' (esto puede ser de gran utilidad para saber a que battallon pertenece)

```sql
SELECT a.id_user, e.battalion,
    CONCAT(a.username, ' ', a.pat_name, ' ', a.mat_name) AS nombre_completo
FROM monitoreo."tbl_user" AS a 
JOIN monitoreo."cat_battalion" AS e
    ON a.id_battalion = e.id_battalion
WHERE e.battalion = 'Celaya'
ORDER BY a.id_user;
```
### Preparando un proceso de réplica y alta disponibilidad.
### Tomando en cuenta la cantidad de registros diarios, actualizaciones en los usuarios y del tipo de información 'sensible', se recomienda realizar una Replicación Síncrona ya que facilita hacer los cambios mediante confirmaciones por al menos un servidor secundario antes de ser confirmados en el servidor primario; sin embargo no por que la opción que nos da sea "fácil" se debe perder de vista  monitorear el estado de la replicación  

```sql
SELECT * FROM pg_stat_replication;
```

### Mayor consistencia a costa de un rendimiento ligeramente inferior.
![alt text](<replica en servidores.png>)
 
### Preparando el monitoreo
### Mantenimiento de la Base de Datos para mantener el buen funcionamiento de PostgreSQL.
### Para este caso es de considerarse el autovacío (vacuum)
### También se considerará el Reindexado y análisis (reindex, analyze)
### Por su contexto ANALYZE en PostgreSQL se utiliza para recopilar estadísticas sobre el contenido de las tablas en la base de datos y almacenar los resultados en el catálogo del sistema pg_statistic. Estas estadísticas son cruciales para que el planificador de consultas de PostgreSQL pueda determinar los planes de ejecución más eficientes para las consultas.

### Funcionamiento de ANALYZE, sin especificar tablas o columnas.
### Si ANALYZE se ejecuta sin una lista específica de tablas o columnas, entonces se procesa automáticamente todas las tablas y vistas materializadas en la base de datos actual a las que el usuario tiene permiso para analizar.

### Especificando tablas, se proporciona una lista de tablas, ANALYZE solo procesará esas tablas especificadas.
### ANALYZE nombre_tabla1, nombre_tabla2;

### Especificando tablas y columnas, es posible afinar aún más el análisis proporcionando una lista de nombres de columnas para una tabla específica. En este caso, ANALYZE recopila estadísticas solo para esas columnas, ANALYZE nombre_tabla (columna1, columna2);esto actualizará las estadísticas de todas las tablas y vistas materializadas que el usuario actual tenga permiso para analizar en la base de datos actual.

### En conclusión beneficios del uso de ANALYZE, mejora del rendimiento de las consultas: El planificador de consultas de PostgreSQL utiliza las estadísticas para estimar el costo de diferentes planes de ejecución y elegir el más eficiente.
### Actualización de estadísticas: Las estadísticas pueden quedar desactualizadas con el tiempo, especialmente en tablas con un alto volumen de operaciones DML (inserciones, actualizaciones, eliminaciones). ANALYZE asegura que las estadísticas reflejen el estado actual de la tabla. Es una buena práctica ejecutar ANALYZE periódicamente, especialmente en bases de datos con mucha actividad, para mantener el rendimiento óptimo de las consultas.


### Migración de datos

### Considera la versión del servidor que manejas, el tipo de información que vas a migrar, si se manejan los mismos gestores de la base de datos, ya que estos pueden variar en cuanto a herramientas.

### Presentación del proyecto

### Un gusto haber presentado, está parte es una grata y entera satisfacción conocer personas tan entregadas a la labor no solo de docencia, sino al desempeño de dentro del ambito laboral, muchas gracias por el conocimiento, pues a pesar de que es aún me falta aprender me voy super agradecida y con más ganas de capacitarme. Mil gracias.