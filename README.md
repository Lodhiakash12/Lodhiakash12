<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Git Dashboard - Interactive README</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: #333;
            line-height: 1.6;
            min-height: 100vh;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        .header {
            text-align: center;
            margin-bottom: 40px;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            backdrop-filter: blur(10px);
        }

        .logo {
            font-size: 3rem;
            font-weight: bold;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 10px;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        .tagline {
            font-size: 1.2rem;
            color: #666;
            margin-bottom: 20px;
        }

        .badges {
            display: flex;
            justify-content: center;
            gap: 10px;
            flex-wrap: wrap;
            margin-top: 20px;
        }

        .badge {
            background: linear-gradient(45deg, #ff9a9e, #fecfef);
            color: white;
            padding: 8px 16px;
            border-radius: 20px;
            font-size: 0.9rem;
            font-weight: bold;
            text-decoration: none;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
        }

        .badge:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3);
        }

        .section {
            background: rgba(255, 255, 255, 0.95);
            margin-bottom: 30px;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            backdrop-filter: blur(10px);
            transition: all 0.3s ease;
        }

        .section:hover {
            transform: translateY(-5px);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
        }

        .section-header {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            padding: 20px;
            cursor: pointer;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: all 0.3s ease;
        }

        .section-header:hover {
            background: linear-gradient(135deg, #5a6fd8, #6a4190);
        }

        .section-header h2 {
            font-size: 1.5rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .toggle-icon {
            font-size: 1.2rem;
            transition: transform 0.3s ease;
        }

        .section-content {
            padding: 30px;
            display: none;
            animation: slideDown 0.3s ease;
        }

        .section-content.active {
            display: block;
        }

        @keyframes slideDown {
            from {
                opacity: 0;
                transform: translateY(-20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .feature-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .feature-card {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            color: white;
            padding: 25px;
            border-radius: 15px;
            text-align: center;
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .feature-card:hover {
            transform: scale(1.05);
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
        }

        .feature-icon {
            font-size: 3rem;
            margin-bottom: 15px;
            display: block;
        }

        .install-tabs {
            display: flex;
            background: #f8f9fa;
            border-radius: 10px;
            overflow: hidden;
            margin-bottom: 20px;
        }

        .tab-button {
            flex: 1;
            padding: 15px;
            background: transparent;
            border: none;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s ease;
        }

        .tab-button.active {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
        }

        .tab-content {
            display: none;
            background: #2d3748;
            color: #e2e8f0;
            padding: 20px;
            border-radius: 10px;
            font-family: 'Courier New', monospace;
            position: relative;
            overflow-x: auto;
        }

        .tab-content.active {
            display: block;
        }

        .copy-btn {
            position: absolute;
            top: 10px;
            right: 10px;
            background: #4a5568;
            color: white;
            border: none;
            padding: 8px 12px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 0.8rem;
            transition: all 0.3s ease;
        }

        .copy-btn:hover {
            background: #2d3748;
        }

        .demo-container {
            background: #1a202c;
            border-radius: 10px;
            padding: 20px;
            margin: 20px 0;
            position: relative;
            overflow: hidden;
        }

        .terminal {
            color: #00ff00;
            font-family: 'Courier New', monospace;
            font-size: 0.9rem;
            line-height: 1.4;
        }

        .cursor {
            animation: blink 1s infinite;
        }

        @keyframes blink {
            0%, 50% { opacity: 1; }
            51%, 100% { opacity: 0; }
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .stat-card {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
            color: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            transition: all 0.3s ease;
        }

        .stat-card:hover {
            transform: translateY(-5px);
        }

        .stat-number {
            font-size: 2rem;
            font-weight: bold;
            display: block;
        }

        .contributors {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 20px;
        }

        .contributor {
            display: flex;
            align-items: center;
            background: #f8f9fa;
            padding: 10px 15px;
            border-radius: 25px;
            transition: all 0.3s ease;
            text-decoration: none;
            color: #333;
        }

        .contributor:hover {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            transform: scale(1.05);
        }

        .avatar {
            width: 30px;
            height: 30px;
            border-radius: 50%;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            margin-right: 10px;
        }

        .progress-bar {
            background: #e2e8f0;
            height: 8px;
            border-radius: 4px;
            overflow: hidden;
            margin: 10px 0;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #4facfe 0%, #00f2fe 100%);
            border-radius: 4px;
            transition: width 2s ease;
        }

        @media (max-width: 768px) {
            .container {
                padding: 10px;
            }
            
            .header {
                padding: 20px;
            }
            
            .logo {
                font-size: 2rem;
            }
            
            .badges {
                flex-direction: column;
                align-items: center;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <div class="logo">🚀 Git Dashboard</div>
            <div class="tagline">A beautiful, interactive dashboard for your Git repositories</div>
            <div class="badges">
                <a href="#" class="badge">⭐ Star on GitHub</a>
                <a href="#" class="badge">📖 Documentation</a>
                <a href="#" class="badge">🐛 Report Bug</a>
                <a href="#" class="badge">💡 Feature Request</a>
            </div>
        </div>

        <div class="section">
            <div class="section-header" onclick="toggleSection(this)">
                <h2>✨ Features</h2>
                <span class="toggle-icon">▼</span>
            </div>
            <div class="section-content">
                <p>Git Dashboard transforms your repository management experience with powerful visualizations and intuitive controls.</p>
                <div class="feature-grid">
                    <div class="feature-card" onclick="showFeatureDemo('commits')">
                        <span class="feature-icon">📊</span>
                        <h3>Commit Analytics</h3>
                        <p>Visualize commit patterns, frequency, and contributor activity with beautiful charts</p>
                    </div>
                    <div class="feature-card" onclick="showFeatureDemo('branches')">
                        <span class="feature-icon">🌿</span>
                        <h3>Branch Management</h3>
                        <p>Interactive branch visualization with merge conflict detection</p>
                    </div>
                    <div class="feature-card" onclick="showFeatureDemo('files')">
                        <span class="feature-icon">📁</span>
                        <h3>File Explorer</h3>
                        <p>Browse repository files with syntax highlighting and diff views</p>
                    </div>
                    <div class="feature-card" onclick="showFeatureDemo('team')">
                        <span class="feature-icon">👥</span>
                        <h3>Team Insights</h3>
                        <p>Track team productivity and collaboration patterns</p>
                    </div>
                </div>
            </div>
        </div>

        <div class="section">
            <div class="section-header" onclick="toggleSection(this)">
                <h2>🚀 Quick Start</h2>
                <span class="toggle-icon">▼</span>
            </div>
            <div class="section-content">
                <div class="install-tabs">
                    <button class="tab-button active" onclick="showTab('npm')">npm</button>
                    <button class="tab-button" onclick="showTab('yarn')">yarn</button>
                    <button class="tab-button" onclick="showTab('docker')">Docker</button>
                </div>
                
                <div class="tab-content active" id="npm">
                    <button class="copy-btn" onclick="copyToClipboard('npm-code')">Copy</button>
                    <pre id="npm-code"># Install Git Dashboard
npm install -g git-dashboard

# Navigate to your repository
cd your-repo

# Launch the dashboard
git-dashboard</pre>
                </div>
                
                <div class="tab-content" id="yarn">
                    <button class="copy-btn" onclick="copyToClipboard('yarn-code')">Copy</button>
                    <pre id="yarn-code"># Install Git Dashboard
yarn global add git-dashboard

# Navigate to your repository
cd your-repo

# Launch the dashboard
git-dashboard</pre>
                </div>
                
                <div class="tab-content" id="docker">
                    <button class="copy-btn" onclick="copyToClipboard('docker-code')">Copy</button>
                    <pre id="docker-code"># Run with Docker
docker run -v $(pwd):/repo -p 3000:3000 git-dashboard

# Or use docker-compose
docker-compose up</pre>
                </div>

                <div class="demo-container">
                    <div class="terminal">
                        <div>$ git-dashboard</div>
                        <div>🚀 Starting Git Dashboard...</div>
                        <div>📊 Analyzing repository...</div>
                        <div>✅ Dashboard ready at http://localhost:3000</div>
                        <div>🎉 Happy coding! <span class="cursor">_</span></div>
                    </div>
                </div>
            </div>
        </div>

        <div class="section">
            <div class="section-header" onclick="toggleSection(this)">
                <h2>📈 Repository Stats</h2>
                <span class="toggle-icon">▼</span>
            </div>
            <div class="section-content">
                <div class="stats-grid">
                    <div class="stat-card">
                        <span class="stat-number" id="commits-count">0</span>
                        <div>Total Commits</div>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: 0%"></div>
                        </div>
                    </div>
                    <div class="stat-card">
                        <span class="stat-number" id="contributors-count">0</span>
                        <div>Contributors</div>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: 0%"></div>
                        </div>
                    </div>
                    <div class="stat-card">
                        <span class="stat-number" id="branches-count">0</span>
                        <div>Branches</div>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: 0%"></div>
                        </div>
                    </div>
                    <div class="stat-card">
                        <span class="stat-number" id="files-count">0</span>
                        <div>Files Tracked</div>
                        <div class="progress-bar">
                            <div class="progress-fill" style="width: 0%"></div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="section">
            <div class="section-header" onclick="toggleSection(this)">
                <h2>🤝 Contributors</h2>
                <span class="toggle-icon">▼</span>
            </div>
            <div class="section-content">
                <p>Thanks to these amazing people who make Git Dashboard possible:</p>
                <div class="contributors">
                    <a href="#" class="contributor">
                        <div class="avatar">JD</div>
                        <div>John Doe</div>
                    </a>
                    <a href="#" class="contributor">
                        <div class="avatar">JS</div>
                        <div>Jane Smith</div>
                    </a>
                    <a href="#" class="contributor">
                        <div class="avatar">AB</div>
                        <div>Alex Brown</div>
                    </a>
                    <a href="#" class="contributor">
                        <div class="avatar">MJ</div>
                        <div>Mike Johnson</div>
                    </a>
                </div>
            </div>
        </div>

        <div class="section">
            <div class="section-header" onclick="toggleSection(this)">
                <h2>📄 License & Support</h2>
                <span class="toggle-icon">▼</span>
            </div>
            <div class="section-content">
                <p>Git Dashboard is released under the MIT License. We welcome contributions, bug reports, and feature requests!</p>
                <div style="margin-top: 20px;">
                    <strong>Support Channels:</strong>
                    <ul style="margin-left: 20px; margin-top: 10px;">
                        <li>📧 Email: support@git-dashboard.dev</li>
                        <li>💬 Discord: Join our community server</li>
                        <li>🐛 Issues: GitHub Issues page</li>
                        <li>📚 Documentation: Official docs site</li>
                    </ul>
                </div>
            </div>
        </div>
    </div>

    <script>
        function toggleSection(header) {
            const content = header.nextElementSibling;
            const icon = header.querySelector('.toggle-icon');
            
            if (content.classList.contains('active')) {
                content.classList.remove('active');
                icon.textContent = '▼';
                icon.style.transform = 'rotate(0deg)';
            } else {
                content.classList.add('active');
                icon.textContent = '▲';
                icon.style.transform = 'rotate(180deg)';
            }
        }

        function showTab(tabName) {
            // Hide all tab contents
            document.querySelectorAll('.tab-content').forEach(content => {
                content.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.tab-button').forEach(button => {
                button.classList.remove('active');
            });
            
            // Show selected tab content
            document.getElementById(tabName).classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
        }

        function copyToClipboard(elementId) {
            const text = document.getElementById(elementId).textContent;
            navigator.clipboard.writeText(text).then(() => {
                const button = event.target;
                const originalText = button.textContent;
                button.textContent = 'Copied!';
                button.style.background = '#48bb78';
                
                setTimeout(() => {
                    button.textContent = originalText;
                    button.style.background = '#4a5568';
                }, 2000);
            });
        }

        function showFeatureDemo(feature) {
            const messages = {
                commits: '📊 Analyzing commit patterns and frequency...',
                branches: '🌿 Visualizing branch structure and merges...',
                files: '📁 Loading file explorer with syntax highlighting...',
                team: '👥 Calculating team collaboration metrics...'
            };
            
            alert(messages[feature] || 'Feature demo coming soon!');
        }

        function animateStats() {
            const stats = [
                { id: 'commits-count', target: 1247, duration: 2000 },
                { id: 'contributors-count', target: 8, duration: 1500 },
                { id: 'branches-count', target: 23, duration: 1800 },
                { id: 'files-count', target: 156, duration: 2200 }
            ];

            stats.forEach((stat, index) => {
                setTimeout(() => {
                    animateNumber(stat.id, stat.target, stat.duration);
                    animateProgressBar(index, stat.duration);
                }, index * 200);
            });
        }

        function animateNumber(elementId, target, duration) {
            const element = document.getElementById(elementId);
            const start = 0;
            const increment = target / (duration / 16);
            let current = start;

            const timer = setInterval(() => {
                current += increment;
                if (current >= target) {
                    current = target;
                    clearInterval(timer);
                }
                element.textContent = Math.floor(current).toLocaleString();
            }, 16);
        }

        function animateProgressBar(index, duration) {
            const progressBars = document.querySelectorAll('.progress-fill');
            const widths = ['85%', '60%', '40%', '75%'];
            
            setTimeout(() => {
                progressBars[index].style.width = widths[index];
            }, 500);
        }

        // Initialize animations when page loads
        window.addEventListener('load', () => {
            // Open first section by default
            const firstSection = document.querySelector('.section-header');
            toggleSection(firstSection);
            
            // Start stats animation after a short delay
            setTimeout(animateStats, 1000);
        });

        // Add some interactive hover effects
        document.querySelectorAll('.feature-card').forEach(card => {
            card.addEventListener('mouseenter', () => {
                card.style.background = 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)';
            });
            
            card.addEventListener('mouseleave', () => {
                card.style.background = 'linear-gradient(135deg, #f093fb 0%, #f5576c 100%)';
            });
        });
    </script>
</body>
</html>
