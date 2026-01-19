const { 
  Client, 
  GatewayIntentBits, 
  ChannelType, 
  PermissionsBitField 
} = require("discord.js");

const client = new Client({
  intents: [
    GatewayIntentBits.Guilds,
    GatewayIntentBits.GuildMessages,
    GatewayIntentBits.MessageContent
  ]
});

const TOKEN = "COLOQUE_SEU_TOKEN_AQUI";

client.on("messageCreate", async (message) => {
  if (message.author.bot) return;

  if (!message.member.permissions.has(PermissionsBitField.Flags.Administrator)) {
    return message.reply("❌ Você precisa ser ADMIN.");
  }

  if (message.content === "!criar") {
    message.reply("⏳ Criando categorias e canais...");

    const guild = message.guild;

    const estrutura = [
      {
        categoria: "📂 Canais & Cargos",
        canais: ["🔒・entregas-automaticas-24h"]
      },
      {
        categoria: "✅ Verificação",
        canais: ["✅・verificação", "⚔️・cofizinpvp"]
      },
      {
        categoria: "🤝 Parcerias",
        canais: ["🤝・parcerias", "🧂・garama-gratis"]
      },
      {
        categoria: "📌 Importante",
        canais: [
          "🏡・boas-vindas",
          "📜・regras",
          "📢・avisos",
          "✉️・invites",
          "🎉・sorteios",
          "👀・spoiler",
          "🔗・seja-staff",
          "🔮・seja-booster",
          "💎・boosters",
          "💎・sorteios-booster",
          "💬・de-uma-sugestão"
        ]
      },
      {
        categoria: "🛒 Produtos",
        canais: [
          "👥・membros",
          "🛒・metodos",
          "💰・metodo-account",
          "🐵・jogue-com-o-cofizin",
          "🧪・scripts"
        ]
      },
      {
        categoria: "🏪 Cofizin Vendedores",
        canais: [
          "💸・alugue-sua-loja",
          "❓・sobre-lojinhas",
          "⭐・vendedores-satisfeitos",
          "✔️・receber-stocks",
          "💎・cofizin-store",
          "🎁・hypezada-store",
          "🎁・ph-store",
          "🎁・felps-store",
          "🎁・benson-store",
          "🎁・zeloto-store"
        ]
      },
      {
        categoria: "🛍️ Comprar",
        canais: ["🎟️・comprar-vendedores"]
      },
      {
        categoria: "⭐ Avaliações",
        canais: [
          "⭐・clientes-satisfeitos",
          "⭐・avaliações-vendedores",
          "⭐・avaliações-middleman"
        ]
      },
      {
        categoria: "🌐 Geral",
        canais: [
          "💭・chat-geral",
          "🤖・comandos",
          "🖼️・midias",
          "🔄・trocas",
          "👥・procurar-time",
          "⚔️・procurar-pvp"
        ]
      },
      {
        categoria: "🎧 Atendimento",
        canais: ["🧾・tickets"]
      }
    ];

    for (const bloco of estrutura) {
      const categoria = await guild.channels.create({
        name: bloco.categoria,
        type: ChannelType.GuildCategory
      });

      for (const canal of bloco.canais) {
        await guild.channels.create({
          name: canal,
          type: ChannelType.GuildText,
          parent: categoria.id
        });
      }
    }

    message.reply("✅ Servidor criado com emojis!");
  }
});

client.once("ready", () => {
  console.log(`🤖 Bot online: ${client.user.tag}`);
});

client.login(TOKEN);
