def gerar_tabelas_escola():
    alunos = [
        (1,  "Carlos Eduardo",   "01", "Turma A"),
        (2,  "Bruno Gomes",      "02", "Turma B"),
        (3,  "Gabriel Mendes",   "03", "Turma A"),
        (4,  "Arthur Alencar",   "04", "Turma C"),
        (5,  "Jose Frazão",      "05", "Turma B"),
        (6,  "Felipe Vieira",    "06", "Turma C"),
        (7,  "Derek Luan",       "07", "Turma A"),
        (8,  "Heitor Alves",     "08", "Turma B"),
        (9,  "Isadora Carvalho", "09", "Turma C"),
        (10, "João Gustavo",     "10", "Turma A"),
    ]

    # (id_professor, nome, área) — IDs de 11 a 99
    professores = [
        (11, "Marcos Antônio Vieira",  "Matemática"),
        (22, "Patrícia Lopes Cunha",   "Língua Portuguesa"),
        (33, "Ricardo Ferreira Nunes", "Ciências"),
        (44, "Simone Dias Carvalho",   "História"),
        (55, "Tiago Borges Macedo",    "Geografia"),
        (66, "Vanessa Pinto Ribeiro",  "Artes"),
        (77, "Anderson Gomes Luz",     "Educação Física"),
        (88, "Beatriz Araújo Mota",    "Inglês"),
        (91, "Cláudio Ramos Figueira", "Física"),
        (99, "Débora Neves Santana",   "Química"),
    ]

    # (id_disciplina, nome, area_especifica, carga_horaria, id_aluno, id_professor)
    disciplinas = [
        (1,  "Matemática",        "Álgebra Linear",        60,  3,  11),
        (2,  "Língua Portuguesa", "Redação e Gramática",   80,  7,  22),
        (3,  "Ciências",          "Biologia Celular",      60,  1,  33),
        (4,  "História",          "Brasil Império",        40,  5,  44),
        (5,  "Geografia",         "Geopolítica Mundial",   40,  9,  55),
        (6,  "Artes",             "Artes Visuais",         40,  2,  66),
        (7,  "Educação Física",   "Atletismo e Saúde",     40,  6,  77),
        (8,  "Inglês",            "Inglês Intermediário",  80,  4,  88),
        (9,  "Física",            "Mecânica Clássica",     60,  8,  91),
        (10, "Química",           "Química Orgânica",      80,  10, 99),
    ]

    SEP      = "+" + "-"*6 + "+" + "-"*28 + "+" + "-"*12 + "+" + "-"*10 + "+"
    SEP_PROF = "+" + "-"*6 + "+" + "-"*28 + "+" + "-"*20 + "+"
    SEP_DISC = "+" + "-"*6 + "+" + "-"*20 + "+" + "-"*24 + "+" + "-"*14 + "+" + "-"*10 + "+" + "-"*9 + "+"
    SEP_REL  = "+" + "-"*10 + "+" + "-"*28 + "+" + "-"*20 + "+" + "-"*9 + "+" + "-"*28 + "+"

    with open("tabelas_escola.txt", "w", encoding="utf-8") as f:

        # ── CABEÇALHO ──────────────────────────────────────────────────────────
        f.write("=" * 70 + "\n")
        f.write("          SISTEMA ESCOLAR\n")
        f.write("=" * 70 + "\n\n")

        # ── TABELA ALUNOS ──────────────────────────────────────────────────────
        f.write("ALUNOS:\n")
        f.write(SEP + "\n")
        f.write(f"| {'ID':<4} | {'Nome Completo':<26} | {'Matrícula':<10} | {'Turma':<8} |\n")
        f.write(SEP + "\n")
        for id_a, nome, matricula, turma in alunos:
            f.write(f"| {str(id_a).zfill(2):<4} | {nome:<26} | {matricula:<10} | {turma:<8} |\n")
        f.write(SEP + "\n\n")

        # ── TABELA PROFESSORES ─────────────────────────────────────────────────
        f.write("PROFESSORES:\n")
        f.write(SEP_PROF + "\n")
        f.write(f"| {'ID':<4} | {'Nome Completo':<26} | {'Área de Atuação':<18} |\n")
        f.write(SEP_PROF + "\n")
        for id_p, nome, area in professores:
            f.write(f"| {id_p:<4} | {nome:<26} | {area:<18} |\n")
        f.write(SEP_PROF + "\n\n")

        # ── TABELA DISCIPLINAS ─────────────────────────────────────────────────
        f.write("DISCIPLINAS:\n")
        f.write(SEP_DISC + "\n")
        f.write(f"| {'ID':<4} | {'Disciplina':<18} | {'Área':<22} | {'Carga Horária':<12} | {'ID_Aluno':<8} | {'ID_Prof':<7} |\n")
        f.write(SEP_DISC + "\n")
        for id_d, nome, area, carga, id_aluno, id_prof in disciplinas:
            f.write(f"| {id_d:<4} | {nome:<18} | {area:<22} | {str(carga) + 'h':<12} | {str(id_aluno).zfill(2):<8} | {id_prof:<7} |\n")
        f.write(SEP_DISC + "\n\n")

        # ── TABELA DE RELACIONAMENTO ───────────────────────────────────────────
        f.write("RELACIONAMENTO:\n")
        f.write(SEP_REL + "\n")
        f.write(f"| {'ID_Aluno':<8} | {'Nome do Aluno':<26} | {'Disciplina':<18} | {'ID_Prof':<7} | {'Nome do Professor':<26} |\n")
        f.write(SEP_REL + "\n")

        id_para_aluno     = {id_a: nome for id_a, nome, _, _  in alunos}
        id_para_professor = {id_p: nome for id_p, nome, _     in professores}

        for id_d, nome_d, area, carga, id_aluno, id_prof in disciplinas:
            nome_aluno = id_para_aluno.get(id_aluno, "—")
            nome_prof  = id_para_professor.get(id_prof, "—")
            f.write(f"| {str(id_aluno).zfill(2):<8} | {nome_aluno:<26} | {nome_d:<18} | {id_prof:<7} | {nome_prof:<26} |\n")

        f.write(SEP_REL + "\n")

    print("Arquivo 'tabelas_escola.txt' gerado com sucesso!")


if __name__ == "__main__":
    gerar_tabelas_escola()
