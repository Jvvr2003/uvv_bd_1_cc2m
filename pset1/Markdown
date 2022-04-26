# Trabalho Pset-1
## Modelo Elmasri
- Comecei meu trabalho pelo modelo elmasri proposto.
![](https://cdn.discordapp.com/attachments/748201102373027931/968623523750895646/unknown.png)
- Fiz apartir do SQL Power Architecht pela máquina virtual.
---
## Script MySQL
- Utilizei MySQL Workbench para produzir o script.
![](https://uploaddeimagens.com.br/images/003/844/307/full/pset23.png?1651007303)
- Após fazer o Esquema do trabalho pelo Workbench utilizei o próprio aplicativo para conseguir o script.
- O script mySQL:
```
-- MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

-- -----------------------------------------------------
-- Esquema projeto1
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `projeto1` DEFAULT CHARACTER SET utf8 ;
USE `projeto1` ;

-- -----------------------------------------------------
-- Criação da tabela `funcionario`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `projeto1`.`funcionario` (
  `cpf` CHAR(11) NOT NULL,
  `primeiro_nome` VARCHAR(15) NULL,
  `nome_meio` CHAR(1) NULL,
  `ultimo_nome` VARCHAR(15) NOT NULL,
  `data_nascimento` DATE NULL,
  `endereco` VARCHAR(30) NULL,
  `sexo` CHAR(1) NULL,
  `salario` DECIMAL(10,2) NULL,
  `cpf_supervisor` CHAR(11) NOT NULL,
  `numero_departamento` INT NOT NULL,
  PRIMARY KEY (`cpf`),
  INDEX `cpf_supervisor_idx` (`cpf_supervisor` ASC) VISIBLE,
  CONSTRAINT `cpf_supervisor`
    FOREIGN KEY (`cpf_supervisor`)
    REFERENCES `projeto1`.`funcionario` (`cpf`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Criação da tabela `departamento`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `projeto1`.`departamento` (
  `numero_departamento` INT NOT NULL,
  `nome_departamento` VARCHAR(15) NOT NULL,
  `cpf_gerente` CHAR(11) NOT NULL,
  `data_inicio_gerente` DATE NULL,
  PRIMARY KEY (`numero_departamento`),
  UNIQUE INDEX `nome_departamento_UNIQUE` (`nome_departamento` ASC) VISIBLE,
  INDEX `cpf_gerente_idx` (`cpf_gerente` ASC) VISIBLE,
  CONSTRAINT `cpf_gerente`
    FOREIGN KEY (`cpf_gerente`)
    REFERENCES `projeto1`.`funcionario` (`cpf`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Criação da tabela `localizacoes_departamento`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `projeto1`.`localizacoes_departamento` (
  `numero_departamento` INT NOT NULL,
  `local` VARCHAR(15) NOT NULL,
  PRIMARY KEY (`local`, `numero_departamento`),
  CONSTRAINT `numero_departamento1`
    FOREIGN KEY (`numero_departamento`)
    REFERENCES `projeto1`.`departamento` (`numero_departamento`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Criação da tabela `dependente`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `projeto1`.`dependente` (
  `cpf_funcionario` CHAR(11) NOT NULL,
  `nome_dependente` VARCHAR(15) NOT NULL,
  `sexo` CHAR(1) NULL,
  `data_nascimento` DATE NULL,
  `parentesco` VARCHAR(15) NULL,
  PRIMARY KEY (`cpf_funcionario`, `nome_dependente`),
  CONSTRAINT `cpf_funcionario2`
    FOREIGN KEY (`cpf_funcionario`)
    REFERENCES `projeto1`.`funcionario` (`cpf`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Criação da tabela `projeto`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `projeto1`.`projeto` (
  `numero_projeto` INT NOT NULL,
  `nome_projeto` VARCHAR(15) NOT NULL,
  `local_projeto` VARCHAR(15) NULL,
  `numero_departamento` INT NOT NULL,
  PRIMARY KEY (`numero_projeto`),
  UNIQUE INDEX `nome_projeto_UNIQUE` (`nome_projeto` ASC) VISIBLE,
  INDEX `numero_departamento_idx` (`numero_departamento` ASC) VISIBLE,
  CONSTRAINT `numero_departamento2`
    FOREIGN KEY (`numero_departamento`)
    REFERENCES `projeto1`.`departamento` (`numero_departamento`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Criação da tabela `trabalha_em`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `projeto1`.`trabalha_em` (
  `cpf_funcionario` CHAR(11) NOT NULL,
  `numero_projeto` INT NOT NULL,
  `horas` DECIMAL(3,1) NOT NULL,
  PRIMARY KEY (`cpf_funcionario`, `numero_projeto`),
  INDEX `numero_projeto_idx` (`numero_projeto` ASC) VISIBLE,
  CONSTRAINT `cpf_funcionario1`
    FOREIGN KEY (`cpf_funcionario`)
    REFERENCES `projeto1`.`funcionario` (`cpf`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `numero_projeto`
    FOREIGN KEY (`numero_projeto`)
    REFERENCES `projeto1`.`projeto` (`numero_projeto`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;

```
---
## Script PostGre
- Utilizei um aplicativo para poder converter para PostGre ([Site do conversor](https://www.convert-in.com/mysql-to-postgres.htm))
- Código após a conversão:
```
/*
Converti de MySQL para PostGre com ajuda de aplicativo
*/
set client_encoding to 'UTF8';

/*
Criação de tabela 'public.departamento'
*/

DROP TABLE IF EXISTS "public"."departamento" CASCADE;
CREATE TABLE "public"."departamento" ("numero_departamento" INTEGER NOT NULL, "nome_departamento" VARCHAR(15)  NOT NULL, "cpf_gerente" VARCHAR(33)  NOT NULL, "data_inicio_gerente" DATE);
DROP INDEX IF EXISTS "PRIMARY";
ALTER TABLE "public"."departamento" ADD CONSTRAINT "PRIMARY" PRIMARY KEY ("numero_departamento");
DROP INDEX IF EXISTS "nome_departamento_UNIQUE";
CREATE UNIQUE INDEX "nome_departamento_UNIQUE" ON "public"."departamento" ("nome_departamento");
DROP INDEX IF EXISTS "cpf_gerente_idx";
CREATE INDEX "cpf_gerente_idx" ON "public"."departamento" ("cpf_gerente");

/*
Dumping data for table 'public.departamento'
*/


/*
Criação de tabela 'public.dependente'
*/

DROP TABLE IF EXISTS "public"."dependente" CASCADE;
CREATE TABLE "public"."dependente" ("cpf_funcionario" VARCHAR(33)  NOT NULL, "nome_dependente" VARCHAR(15)  NOT NULL, "sexo" VARCHAR(3) , "data_nascimento" DATE, "parentesco" VARCHAR(15) );
DROP INDEX IF EXISTS "PRIMARY00000";
ALTER TABLE "public"."dependente" ADD CONSTRAINT "PRIMARY00000" PRIMARY KEY ("cpf_funcionario", "nome_dependente");

/*
Dumping data for table 'public.dependente'
*/

/*
Criação de tabela 'public.funcionario'
*/

DROP TABLE IF EXISTS "public"."funcionario" CASCADE;
CREATE TABLE "public"."funcionario" ("cpf" VARCHAR(33)  NOT NULL, "primeiro_nome" VARCHAR(15) , "nome_meio" VARCHAR(3) , "ultimo_nome" VARCHAR(15)  NOT NULL, "data_nascimento" DATE, "endereco" VARCHAR(30) , "sexo" VARCHAR(3) , "salario" DECIMAL(10,2), "cpf_supervisor" VARCHAR(33)  NOT NULL, "numero_departamento" INTEGER NOT NULL);
DROP INDEX IF EXISTS "PRIMARY00001";
ALTER TABLE "public"."funcionario" ADD CONSTRAINT "PRIMARY00001" PRIMARY KEY ("cpf");
DROP INDEX IF EXISTS "cpf_supervisor_idx";
CREATE INDEX "cpf_supervisor_idx" ON "public"."funcionario" ("cpf_supervisor");

/*
Dumping data for table 'public.funcionario'
*/


/*
Criação de tabela 'public.localizacoes_departamento'
*/

DROP TABLE IF EXISTS "public"."localizacoes_departamento" CASCADE;
CREATE TABLE "public"."localizacoes_departamento" ("numero_departamento" INTEGER NOT NULL, "local" VARCHAR(15)  NOT NULL);
DROP INDEX IF EXISTS "PRIMARY00002";
ALTER TABLE "public"."localizacoes_departamento" ADD CONSTRAINT "PRIMARY00002" PRIMARY KEY ("numero_departamento", "local");

/*
Dumping data for table 'public.localizacoes_departamento'
*/


/*
Criação de tabela 'public.projeto'
*/

DROP TABLE IF EXISTS "public"."projeto" CASCADE;
CREATE TABLE "public"."projeto" ("numero_projeto" INTEGER NOT NULL, "nome_projeto" VARCHAR(15)  NOT NULL, "local_projeto" VARCHAR(15) , "numero_departamen" INTEGER NOT NULL);
DROP INDEX IF EXISTS "PRIMARY00003";
ALTER TABLE "public"."projeto" ADD CONSTRAINT "PRIMARY00003" PRIMARY KEY ("numero_projeto");
DROP INDEX IF EXISTS "nome_projeto_UNIQUE";
CREATE UNIQUE INDEX "nome_projeto_UNIQUE" ON "public"."projeto" ("nome_projeto");
DROP INDEX IF EXISTS "numero_departamento_idx";
CREATE INDEX "numero_departamento_idx" ON "public"."projeto" ("numero_departamen");

/*
Dumping data for table 'public.projeto'
*/


/*
Criação de tabela 'public.trabalha_em'
*/

DROP TABLE IF EXISTS "public"."trabalha_em" CASCADE;
CREATE TABLE "public"."trabalha_em" ("cpf_funcionario" VARCHAR(33)  NOT NULL, "numero_projeto" INTEGER NOT NULL, "horas" DECIMAL(3,1) NOT NULL);
DROP INDEX IF EXISTS "PRIMARY00004";
ALTER TABLE "public"."trabalha_em" ADD CONSTRAINT "PRIMARY00004" PRIMARY KEY ("cpf_funcionario", "numero_projeto");
DROP INDEX IF EXISTS "numero_projeto_idx";
CREATE INDEX "numero_projeto_idx" ON "public"."trabalha_em" ("numero_projeto");

/*
Dumping data for table 'public.trabalha_em'
*/
```
---
## Observações
- Este trabalho foi feito com Rodrigo Fassarella Leite
