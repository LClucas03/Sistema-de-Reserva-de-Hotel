# Sistema-de-Reserva-de-Hotel

CRIAR BANCO DE DADOS HotelReservation;
USE Reserva de Hotel;
CRIAR TABELA Convidados (
    guest_id INT AUTO_INCREMENTO CHAVE PRIMÁRIA,
    first_name VARCHAR(50) NÃO NULO,
    sobrenome VARCHAR(50) NÃO NULO,
    e-mail VARCHAR(100) ÚNICO NÃO NULO,
    telefone VARCHAR(20)
);
CRIAR TABELA Salas (
    room_id INT INCREMENTO AUTOMÁTICO CHAVE PRIMÁRIA,
    room_number VARCHAR(10) ÚNICO NÃO NULO,
    room_type VARCHAR(50) NÃO NULO,
    preço DECIMAL(10, 2) NÃO NULO,
    status ENUM('disponível', 'ocupado', 'manutenção') PADRÃO 'disponível'
);
CRIAR TABELA Reservas (
    reservation_id INT INCREMENTO AUTOMÁTICO CHAVE PRIMÁRIA,
    guest_id INT,
    room_id INT,
    check_in DATA NÃO NULA,
    check_out DATA NÃO NULA,
    reservation_date CARIMBO DE DATA/HORA PADRÃO CARIMBO DE DATA/HORA ATUAL,
    status ENUM('confirmado', 'check-in', 'check-out', 'cancelado') PADRÃO 'confirmado',
    REFERÊNCIAS DE CHAVE ESTRANGEIRA (guest_id) Convidados(guest_id),
    CHAVE ESTRANGEIRA (room_id) REFERÊNCIAS Quartos(room_id)
);
INSERIR EM Convidados (nome, sobrenome, e-mail, telefone)
VALORES ('João', 'Silva', 'joão.silva@exemplo.com', '123-456-7890');
INSERIR EM Quartos (número_quarto, tipo_quarto, preço)
VALORES ('101', 'Único', 100,00),
       ('102', 'Duplo', 150,00),
       ('103', 'Suíte', 250,00);
INSERIR EM Reservas (guest_id, room_id, check_in, check_out)
VALORES (1, 1, '2024-10-01', '2024-10-05');
SELECIONE * DE Convidados;
SELECIONE * DE Salas ONDE status = 'disponível';
SELECIONE r.reservation_id, g.first_name, g.last_name, ro.room_number, r.check_in, r.check_out
DE Reservas r
JUNTE-SE A CONVIDADOS g ON r.guest_id = g.guest_id
JUNTE-SE às salas ro ON r.room_id = ro.room_id
ONDE g.email = 'john.doe@example.com';
ATUALIZAÇÃO Quartos
Status SET = 'ocupado'
ONDE room_id = 1;
ATUALIZAÇÃO Convidados
SET telefone = '987-654-3210'
ONDE email = 'john.doe@example.com';
EXCLUIR DE Reservas
ONDE reservation_id = 1;
EXCLUIR DE Convidados
ONDE email = 'john.doe@example.com';
