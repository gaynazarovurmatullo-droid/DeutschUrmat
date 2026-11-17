# DeutschUrmat
import 'package:flutter/material.dart';

void main() {
  runApp(const DeutschUrmat());
}

class DeutschUrmat extends StatelessWidget {
  const DeutschUrmat({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'DeutschUrmat',
      theme: ThemeData(
        colorSchemeSeed: Colors.blue,
        useMaterial3: true,
      ),
      home: const HomePage(),
    );
  }
}

class HomePage extends StatefulWidget {
  const HomePage({super.key});

  @override
  State<HomePage> createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  bool kyrgyz = true;

  final levels = ['A1', 'A2', 'B1', 'B2'];

  final sections = [
    {'icon': Icons.menu_book, 'ky': 'Окуу', 'de': 'Lesen'},
    {'icon': Icons.headphones, 'ky': 'Угуу', 'de': 'Hören'},
    {'icon': Icons.edit, 'ky': 'Жазуу', 'de': 'Schreiben'},
    {'icon': Icons.mic, 'ky': 'Сүйлөө', 'de': 'Sprechen'},
    {'icon': Icons.translate, 'ky': 'Сөздүк', 'de': 'Wortschatz'},
    {'icon': Icons.quiz, 'ky': 'Тест', 'de': 'Prüfungstest'},
  ];

  String selectedLevel = 'A1';

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text(
          'DeutschUrmat 🇩🇪',
          style: TextStyle(fontWeight: FontWeight.bold),
        ),
        actions: [
          TextButton(
            onPressed: () {
              setState(() => kyrgyz = !kyrgyz);
            },
            child: Text(kyrgyz ? '🇰🇬 KG' : '🇩🇪 DE'),
          ),
        ],
      ),
      body: ListView(
        padding: const EdgeInsets.all(16),
        children: [
          Container(
            padding: const EdgeInsets.all(20),
            decoration: BoxDecoration(
              color: Colors.blue.shade700,
              borderRadius: BorderRadius.circular(20),
            ),
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                const Text(
                  'Willkommen!',
                  style: TextStyle(
                    color: Colors.white,
                    fontSize: 25,
                    fontWeight: FontWeight.bold,
                  ),
                ),
                const SizedBox(height: 8),
                Text(
                  kyrgyz
                      ? 'Немис тилин биз менен үйрөн!'
                      : 'Lerne Deutsch mit uns!',
                  style: const TextStyle(
                    color: Colors.white,
                    fontSize: 16,
                  ),
                ),
              ],
            ),
          ),
          const SizedBox(height: 24),
          Text(
            kyrgyz ? 'Деңгээлиңди танда' : 'Wähle dein Niveau',
            style: const TextStyle(
              fontSize: 20,
              fontWeight: FontWeight.bold,
            ),
          ),
          const SizedBox(height: 12),
          Wrap(
            spacing: 10,
            children: levels.map((level) {
              return ChoiceChip(
                label: Text(level),
                selected: selectedLevel == level,
                onSelected: (_) {
                  setState(() => selectedLevel = level);
                },
              );
            }).toList(),
          ),
          const SizedBox(height: 24),
          Text(
            kyrgyz ? 'Сабактар' : 'Lektionen',
            style: const TextStyle(
              fontSize: 20,
              fontWeight: FontWeight.bold,
            ),
          ),
          const SizedBox(height: 12),
          GridView.builder(
            shrinkWrap: true,
            physics: const NeverScrollableScrollPhysics(),
            itemCount: sections.length,
            gridDelegate:
                const SliverGridDelegateWithFixedCrossAxisCount(
              crossAxisCount: 2,
              crossAxisSpacing: 12,
              mainAxisSpacing: 12,
              childAspectRatio: 1.25,
            ),
            itemBuilder: (context, index) {
              final section = sections[index];
              return Card(
                child: InkWell(
                  borderRadius: BorderRadius.circular(12),
                  onTap: () {
                    ScaffoldMessenger.of(context).showSnackBar(
                      SnackBar(
                        content: Text(
                          '${section[kyrgyz ? 'ky' : 'de']} - $selectedLevel',
                        ),
                      ),
                    );
                  },
                  child: Column(
                    mainAxisAlignment: MainAxisAlignment.center,
                    children: [
                      Icon(
                        section['icon'] as IconData,
                        size: 35,
                        color: Colors.blue,
                      ),
                      const SizedBox(height: 10),
                      Text(
                        section[kyrgyz ? 'ky' : 'de'] as String,
                        style: const TextStyle(
                          fontSize: 16,
                          fontWeight: FontWeight.bold,
                        ),
                      ),
                    ],
                  ),
                ),
              );
            },
          ),
        ],
      ),
    );
  }
}
