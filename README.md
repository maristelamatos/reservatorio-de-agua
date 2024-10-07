# reservatorio-de-agua
class Program
{
    	static void Main(string[] args)
	{
		while (true)
		{
			VerificarSistema();
			if (sistemaEmErro)
			{
				Console.WriteLine("Erro no sistema: Bomba e Eletroválvula não acionadas.");
				continue;
			}

			// Acionar a eletroválvula S2 se a boia B não estiver acionada
			if (!boiaBAtivada)
			{
				AcionarEletrovalvula();
			}

			// Acionar a bomba se o nível de água estiver abaixo da boia C
			if (nivelReservatorio < 20) // Nível mínimo (boia C)
			{
				AcionarBomba();
			}

			// Exibir estado atual do sistema
			ExibirEstado();
			Console.WriteLine("Pressione Enter para continuar...");
			Console.ReadLine();
		}
	}

	static void VerificarSistema()
	{
		if (nivelReservatorio < 0 || nivelReservatorio > capacidadeReservatorio)
		{
			sistemaEmErro = true;
		}
		else
		{
			sistemaEmErro = false;
		}
	}

	static void AcionarEletrovalvula()
	{
		if (nivelReservatorio < capacidadeReservatorio)
		{
			nivelReservatorio += 10; // Simulando a entrada de água
			Console.WriteLine("Eletroválvula acionada: Nível do reservatório agora é " + nivelReservatorio + " litros.");
		}
	}

	static void AcionarBomba()
	{
		if (nivelReservatorio > 0) // Verifica se o reservatório não está vazio
		{
			nivelReservatorio -= 5; // Simulando a saída de água
			Console.WriteLine("Bomba acionada: Nível do reservatório agora é " + nivelReservatorio + " litros.");
		}
		else
		{
			Console.WriteLine("A bomba não pode ser acionada: Reservatório vazio.");
		}
	}

	static void ExibirEstado()
	{
		Console.WriteLine($"Nível do reservatório: {nivelReservatorio} litros.");
		Console.WriteLine($"Boia B ativada: {boiaBAtivada}");
		Console.WriteLine($"Boia C ativada: {boiaCAtivada}");
		Console.WriteLine($"Sistema em erro: {sistemaEmErro}");
	}
}