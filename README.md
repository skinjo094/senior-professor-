<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Senior Inbound Professor Promotion Tracker - Spreadsheet</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #f5f7fa;
            padding: 20px;
            line-height: 1.4;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            background: white;
            border-radius: 10px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #2c3e50, #3498db);
            color: white;
            padding: 20px;
            text-align: center;
        }

        .header h1 {
            font-size: 1.8em;
            margin-bottom: 5px;
        }

        .header p {
            font-size: 0.9em;
            opacity: 0.9;
        }

        .summary-section {
            background: #f8f9fa;
            padding: 20px;
            border-bottom: 2px solid #e9ecef;
        }

        .summary-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }

        .summary-card {
            background: white;
            padding: 15px;
            border-radius: 8px;
            text-align: center;
            box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
        }

        .summary-card h3 {
            color: #2c3e50;
            font-size: 1em;
            margin-bottom: 8px;
        }

        .score {
            font-size: 1.5em;
            font-weight: bold;
            color: #3498db;
        }

        .spreadsheet-table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.85em;
        }

        .spreadsheet-table th,
        .spreadsheet-table td {
            border: 1px solid #dee2e6;
            padding: 8px;
            text-align: left;
            vertical-align: top;
        }

        .spreadsheet-table th {
            background: #f8f9fa;
            font-weight: 600;
            color: #495057;
            position: sticky;
            top: 0;
            z-index: 10;
        }

        .category-header {
            background: #e9ecef !important;
            font-weight: bold;
            color: #2c3e50 !important;
            text-align: center;
        }

        .status-cell {
            width: 120px;
            text-align: center;
        }

        .status-select {
            width: 100%;
            padding: 4px;
            border: 1px solid #ced4da;
            border-radius: 4px;
            font-size: 0.8em;
        }

        .evidence-cell {
            width: 250px;
        }

        .evidence-textarea {
            width: 100%;
            min-height: 60px;
            padding: 6px;
            border: 1px solid #ced4da;
            border-radius: 4px;
            font-size: 0.8em;
            resize: vertical;
            font-family: inherit;
        }

        .manager-textarea {
            background: #f8fbff;
            border-color: #3498db;
        }

        .score-cell {
            width: 60px;
            text-align: center;
            font-weight: bold;
        }

        .requirement-title {
            font-weight: 600;
            color: #2c3e50;
            max-width: 200px;
        }

        .requirement-description {
            color: #6c757d;
            font-size: 0.8em;
            margin-top: 4px;
        }

        .status-leading { background: #d4edda; color: #155724; }
        .status-working { background: #fff3cd; color: #856404; }
        .status-opportunity { background: #f8d7da; color: #721c24; }
        .status-no-opportunity { background: #e2e3e4; color: #383d41; }

        .actions-section {
            background: #f8f9fa;
            padding: 20px;
            border-top: 2px solid #e9ecef;
        }

        .actions-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
        }

        .action-card {
            background: white;
            padding: 15px;
            border-radius: 8px;
            box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
        }

        .action-card h3 {
            color: #2c3e50;
            margin-bottom: 10px;
            font-size: 1em;
        }

        .action-textarea {
            width: 100%;
            min-height: 80px;
            padding: 10px;
            border: 1px solid #ced4da;
            border-radius: 4px;
            font-size: 0.85em;
            resize: vertical;
            font-family: inherit;
        }

        .export-section {
            text-align: center;
            padding: 20px;
            background: #f8f9fa;
        }

        .export-btn {
            background: linear-gradient(135deg, #3498db, #2ecc71);
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 20px;
            font-size: 1em;
            cursor: pointer;
            transition: transform 0.2s ease;
        }

        .export-btn:hover {
            transform: translateY(-2px);
        }

        .table-container {
            overflow-x: auto;
            max-height: 70vh;
            overflow-y: auto;
        }

        @media (max-width: 768px) {
            .container {
                margin: 10px;
            }
            
            .summary-grid {
                grid-template-columns: 1fr;
            }
            
            .actions-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>Senior Inbound Professor Promotion Tracker</h1>
            <p>Collaborative Assessment Spreadsheet</p>
        </div>

        <div class="summary-section">
            <div class="summary-grid">
                <div class="summary-card">
                    <h3>Overall Readiness</h3>
                    <div class="score" id="overall-score">0%</div>
                </div>
                <div class="summary-card">
                    <h3>Impact</h3>
                    <div class="score" id="impact-score">0%</div>
                </div>
                <div class="summary-card">
                    <h3>Influence</h3>
                    <div class="score" id="influence-score">0%</div>
                </div>
                <div class="summary-card">
                    <h3>Expertise</h3>
                    <div class="score" id="expertise-score">0%</div>
                </div>
                <div class="summary-card">
                    <h3>Core Attributes</h3>
                    <div class="score" id="attributes-score">0%</div>
                </div>
            </div>
        </div>

        <div class="table-container">
            <table class="spreadsheet-table">
                <thead>
                    <tr>
                        <th style="width: 80px;">Category</th>
                        <th style="width: 200px;">Requirement</th>
                        <th style="width: 120px;">Status</th>
                        <th style="width: 60px;">Score</th>
                        <th style="width: 250px;">Employee Evidence</th>
                        <th style="width: 250px;">Manager Reflections</th>
                    </tr>
                </thead>
                <tbody id="requirements-table">
                    <!-- Impact Requirements -->
                    <tr class="category-header">
                        <td colspan="6">IMPACT</td>
                    </tr>
                    <tr data-category="impact">
                        <td>Impact</td>
                        <td>
                            <div class="requirement-title">Strategic Information Gathering & Decision Making</div>
                            <div class="requirement-description">Focuses on gathering and distilling information from multiple sources--internal and external--to make short and long-term strategic decisions for the team</div>
                        </td>
                        <td class="status-cell">
                            <select class="status-select" onchange="updateStatus(this)">
                                <option value="opportunity">Opportunity</option>
                                <option value="working">Working On</option>
                                <option value="leading">Leading</option>
                                <option value="no-opportunity">No Opportunity</option>
                            </select>
                        </td>
                        <td class="score-cell">1</td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea" placeholder="Provide specific examples of how you gather information from multiple sources and use it for strategic decision-making..." oninput="saveData()"></textarea>
                        </td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea manager-textarea" placeholder="Manager's observations, feedback, and additional context..." oninput="saveData()"></textarea>
                        </td>
                    </tr>
                    <tr data-category="impact">
                        <td>Impact</td>
                        <td>
                            <div class="requirement-title">Project Prioritization & Communication</div>
                            <div class="requirement-description">Capable of prioritizing largest impact projects effectively, and managing up through communicating decision-making process of what projects they aren't able to take on</div>
                        </td>
                        <td class="status-cell">
                            <select class="status-select" onchange="updateStatus(this)">
                                <option value="opportunity">Opportunity</option>
                                <option value="working">Working On</option>
                                <option value="leading">Leading</option>
                                <option value="no-opportunity">No Opportunity</option>
                            </select>
                        </td>
                        <td class="score-cell">1</td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea" placeholder="Describe how you prioritize projects and communicate with leadership about project decisions..." oninput="saveData()"></textarea>
                        </td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea manager-textarea" placeholder="Manager's observations, feedback, and additional context..." oninput="saveData()"></textarea>
                        </td>
                    </tr>
                    <tr data-category="impact">
                        <td>Impact</td>
                        <td>
                            <div class="requirement-title">Program Ownership</div>
                            <div class="requirement-description">Generally owns multiple programs or one program with many facets</div>
                        </td>
                        <td class="status-cell">
                            <select class="status-select" onchange="updateStatus(this)">
                                <option value="opportunity">Opportunity</option>
                                <option value="working">Working On</option>
                                <option value="leading">Leading</option>
                                <option value="no-opportunity">No Opportunity</option>
                            </select>
                        </td>
                        <td class="score-cell">1</td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea" placeholder="List the programs you currently own and their complexity/scope..." oninput="saveData()"></textarea>
                        </td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea manager-textarea" placeholder="Manager's observations, feedback, and additional context..." oninput="saveData()"></textarea>
                        </td>
                    </tr>
                    <tr data-category="impact">
                        <td>Impact</td>
                        <td>
                            <div class="requirement-title">Complex Problem Analysis</div>
                            <div class="requirement-description">Works on problems of diverse scope where analysis of data requires evaluation of identifiable factors</div>
                        </td>
                        <td class="status-cell">
                            <select class="status-select" onchange="updateStatus(this)">
                                <option value="opportunity">Opportunity</option>
                                <option value="working">Working On</option>
                                <option value="leading">Leading</option>
                                <option value="no-opportunity">No Opportunity</option>
                            </select>
                        </td>
                        <td class="score-cell">1</td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea" placeholder="Provide examples of complex problems you've analyzed and the factors you considered..." oninput="saveData()"></textarea>
                        </td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea manager-textarea" placeholder="Manager's observations, feedback, and additional context..." oninput="saveData()"></textarea>
                        </td>
                    </tr>
                    <tr data-category="impact">
                        <td>Impact</td>
                        <td>
                            <div class="requirement-title">Innovation & Implementation</div>
                            <div class="requirement-description">Consistently brings new ideas and helps team implement them to improve processes or outcomes. Can present cross-functionally to share ideas and drive adoption</div>
                        </td>
                        <td class="status-cell">
                            <select class="status-select" onchange="updateStatus(this)">
                                <option value="opportunity">Opportunity</option>
                                <option value="working">Working On</option>
                                <option value="leading">Leading</option>
                                <option value="no-opportunity">No Opportunity</option>
                            </select>
                        </td>
                        <td class="score-cell">1</td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea" placeholder="Detail specific innovations you've introduced and how you've driven their adoption..." oninput="saveData()"></textarea>
                        </td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea manager-textarea" placeholder="Manager's observations, feedback, and additional context..." oninput="saveData()"></textarea>
                        </td>
                    </tr>

                    <!-- Influence Requirements -->
                    <tr class="category-header">
                        <td colspan="6">INFLUENCE</td>
                    </tr>
                    <tr data-category="influence">
                        <td>Influence</td>
                        <td>
                            <div class="requirement-title">Cross-Functional Relationship Building</div>
                            <div class="requirement-description">Builds productive relationships with key contacts at various levels of authority outside own area of expertise</div>
                        </td>
                        <td class="status-cell">
                            <select class="status-select" onchange="updateStatus(this)">
                                <option value="opportunity">Opportunity</option>
                                <option value="working">Working On</option>
                                <option value="leading">Leading</option>
                                <option value="no-opportunity">No Opportunity</option>
                            </select>
                        </td>
                        <td class="score-cell">1</td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea" placeholder="Describe key relationships you've built outside your expertise area and their impact..." oninput="saveData()"></textarea>
                        </td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea manager-textarea" placeholder="Manager's observations, feedback, and additional context..." oninput="saveData()"></textarea>
                        </td>
                    </tr>
                    <tr data-category="influence">
                        <td>Influence</td>
                        <td>
                            <div class="requirement-title">Cross-Functional Team Leadership</div>
                            <div class="requirement-description">Effectively spearheads cross-functional teams on multi-faceted projects by leading through influence</div>
                        </td>
                        <td class="status-cell">
                            <select class="status-select" onchange="updateStatus(this)">
                                <option value="opportunity">Opportunity</option>
                                <option value="working">Working On</option>
                                <option value="leading">Leading</option>
                                <option value="no-opportunity">No Opportunity</option>
                            </select>
                        </td>
                        <td class="score-cell">1</td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea" placeholder="Provide examples of cross-functional teams you've led and how you influenced outcomes..." oninput="saveData()"></textarea>
                        </td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea manager-textarea" placeholder="Manager's observations, feedback, and additional context..." oninput="saveData()"></textarea>
                        </td>
                    </tr>
                    <tr data-category="influence">
                        <td>Influence</td>
                        <td>
                            <div class="requirement-title">Mentoring & Team Development</div>
                            <div class="requirement-description">May regularly mentor other team members who are developing skills and is seen as a leader on the team</div>
                        </td>
                        <td class="status-cell">
                            <select class="status-select" onchange="updateStatus(this)">
                                <option value="opportunity">Opportunity</option>
                                <option value="working">Working On</option>
                                <option value="leading">Leading</option>
                                <option value="no-opportunity">No Opportunity</option>
                            </select>
                        </td>
                        <td class="score-cell">1</td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea" placeholder="Describe your mentoring activities and leadership recognition within the team..." oninput="saveData()"></textarea>
                        </td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea manager-textarea" placeholder="Manager's observations, feedback, and additional context..." oninput="saveData()"></textarea>
                        </td>
                    </tr>

                    <!-- Expertise Requirements -->
                    <tr class="category-header">
                        <td colspan="6">EXPERTISE</td>
                    </tr>
                    <tr data-category="expertise">
                        <td>Expertise</td>
                        <td>
                            <div class="requirement-title">Specialized Knowledge & Problem Solving</div>
                            <div class="requirement-description">A seasoned, experienced professional with full understanding of area of specialization; capable of resolving wide range of issues in creative ways</div>
                        </td>
                        <td class="status-cell">
                            <select class="status-select" onchange="updateStatus(this)">
                                <option value="opportunity">Opportunity</option>
                                <option value="working">Working On</option>
                                <option value="leading">Leading</option>
                                <option value="no-opportunity">No Opportunity</option>
                            </select>
                        </td>
                        <td class="score-cell">1</td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea" placeholder="Demonstrate your specialized knowledge and creative problem-solving abilities..." oninput="saveData()"></textarea>
                        </td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea manager-textarea" placeholder="Manager's observations, feedback, and additional context..." oninput="saveData()"></textarea>
                        </td>
                    </tr>
                    <tr data-category="expertise">
                        <td>Expertise</td>
                        <td>
                            <div class="requirement-title">Strategic Recommendations</div>
                            <div class="requirement-description">Makes informed recommendations for solutions when major potholes present themselves</div>
                        </td>
                        <td class="status-cell">
                            <select class="status-select" onchange="updateStatus(this)">
                                <option value="opportunity">Opportunity</option>
                                <option value="working">Working On</option>
                                <option value="leading">Leading</option>
                                <option value="no-opportunity">No Opportunity</option>
                            </select>
                        </td>
                        <td class="score-cell">1</td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea" placeholder="Provide examples of strategic recommendations you've made during challenging situations..." oninput="saveData()"></textarea>
                        </td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea manager-textarea" placeholder="Manager's observations, feedback, and additional context..." oninput="saveData()"></textarea>
                        </td>
                    </tr>
                    <tr data-category="expertise">
                        <td>Expertise</td>
                        <td>
                            <div class="requirement-title">Internal & External Recognition</div>
                            <div class="requirement-description">Is starting to be identified internally as an expert and developing external brand recognition</div>
                        </td>
                        <td class="status-cell">
                            <select class="status-select" onchange="updateStatus(this)">
                                <option value="opportunity">Opportunity</option>
                                <option value="working">Working On</option>
                                <option value="leading">Leading</option>
                                <option value="no-opportunity">No Opportunity</option>
                            </select>
                        </td>
                        <td class="score-cell">1</td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea" placeholder="Document internal recognition and external brand-building activities..." oninput="saveData()"></textarea>
                        </td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea manager-textarea" placeholder="Manager's observations, feedback, and additional context..." oninput="saveData()"></textarea>
                        </td>
                    </tr>

                    <!-- Core Attributes Requirements -->
                    <tr class="category-header">
                        <td colspan="6">CORE ATTRIBUTES</td>
                    </tr>
                    <tr data-category="attributes">
                        <td>Attributes</td>
                        <td>
                            <div class="requirement-title">Depth of Knowledge (Expertise)</div>
                            <div class="requirement-description">Possesses depth in a particular area and can be relied upon to be a subject matter expert</div>
                        </td>
                        <td class="status-cell">
                            <select class="status-select" onchange="updateStatus(this)">
                                <option value="opportunity">Opportunity</option>
                                <option value="working">Working On</option>
                                <option value="leading">Leading</option>
                                <option value="no-opportunity">No Opportunity</option>
                            </select>
                        </td>
                        <td class="score-cell">1</td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea" placeholder="Detail your subject matter expertise and how others rely on your knowledge..." oninput="saveData()"></textarea>
                        </td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea manager-textarea" placeholder="Manager's observations, feedback, and additional context..." oninput="saveData()"></textarea>
                        </td>
                    </tr>
                    <tr data-category="attributes">
                        <td>Attributes</td>
                        <td>
                            <div class="requirement-title">Driving Results</div>
                            <div class="requirement-description">Desire and excited by meeting and exceeding expectations and objectives. Aims to improve own performance and that of the business or customer</div>
                        </td>
                        <td class="status-cell">
                            <select class="status-select" onchange="updateStatus(this)">
                                <option value="opportunity">Opportunity</option>
                                <option value="working">Working On</option>
                                <option value="leading">Leading</option>
                                <option value="no-opportunity">No Opportunity</option>
                            </select>
                        </td>
                        <td class="score-cell">1</td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea" placeholder="Provide examples of exceeding expectations and driving performance improvements..." oninput="saveData()"></textarea>
                        </td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea manager-textarea" placeholder="Manager's observations, feedback, and additional context..." oninput="saveData()"></textarea>
                        </td>
                    </tr>
                    <tr data-category="attributes">
                        <td>Attributes</td>
                        <td>
                            <div class="requirement-title">Change Leadership</div>
                            <div class="requirement-description">Ability to align an organization, team or key stakeholders through needed change to drive performance and results</div>
                        </td>
                        <td class="status-cell">
                            <select class="status-select" onchange="updateStatus(this)">
                                <option value="opportunity">Opportunity</option>
                                <option value="working">Working On</option>
                                <option value="leading">Leading</option>
                                <option value="no-opportunity">No Opportunity</option>
                            </select>
                        </td>
                        <td class="score-cell">1</td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea" placeholder="Describe how you've led change initiatives and aligned stakeholders..." oninput="saveData()"></textarea>
                        </td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea manager-textarea" placeholder="Manager's observations, feedback, and additional context..." oninput="saveData()"></textarea>
                        </td>
                    </tr>
                    <tr data-category="attributes">
                        <td>Attributes</td>
                        <td>
                            <div class="requirement-title">Vision Setting (Thought Leadership)</div>
                            <div class="requirement-description">Can create and share a compelling picture of the needed strategy/action/program that motivates others to act</div>
                        </td>
                        <td class="status-cell">
                            <select class="status-select" onchange="updateStatus(this)">
                                <option value="opportunity">Opportunity</option>
                                <option value="working">Working On</option>
                                <option value="leading">Leading</option>
                                <option value="no-opportunity">No Opportunity</option>
                            </select>
                        </td>
                        <td class="score-cell">1</td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea" placeholder="Share examples of visions you've created and how they motivated action..." oninput="saveData()"></textarea>
                        </td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea manager-textarea" placeholder="Manager's observations, feedback, and additional context..." oninput="saveData()"></textarea>
                        </td>
                    </tr>
                    <tr data-category="attributes">
                        <td>Attributes</td>
                        <td>
                            <div class="requirement-title">Customer-First Mentality</div>
                            <div class="requirement-description">Building strong customer relationships and seeking solutions that help the customer. Actively pays attention to needs and is adaptable and proactive</div>
                        </td>
                        <td class="status-cell">
                            <select class="status-select" onchange="updateStatus(this)">
                                <option value="opportunity">Opportunity</option>
                                <option value="working">Working On</option>
                                <option value="leading">Leading</option>
                                <option value="no-opportunity">No Opportunity</option>
                            </select>
                        </td>
                        <td class="score-cell">1</td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea" placeholder="Demonstrate your customer-first approach with specific examples..." oninput="saveData()"></textarea>
                        </td>
                        <td class="evidence-cell">
                            <textarea class="evidence-textarea manager-textarea" placeholder="Manager's observations, feedback, and additional context..." oninput="saveData()"></textarea>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>

        <div class="actions-section">
            <div class="actions-grid">
                <div class="action-card">
                    <h3>Development Action Items</h3>
                    <textarea class="action-textarea" id="action-items" placeholder="List specific actions you need to take to strengthen areas where you're not fully meeting requirements..." oninput="saveData()"></textarea>
                </div>
                <div class="action-card">
                    <h3>Discussion Points for Manager Meeting</h3>
                    <textarea class="action-textarea" id="discussion-points" placeholder="Note key points to discuss with your manager about this promotion..." oninput="saveData()"></textarea>
                </div>
                <div class="action-card">
                    <h3>Additional Notes</h3>
                    <textarea class="action-textarea" id="additional-notes" placeholder="Any other thoughts, observations, or preparation notes..." oninput="saveData()"></textarea>
                </div>
            </div>
        </div>

        <div class="export-section">
            <button class="export-btn" onclick="exportToCSV()">Export to CSV</button>
            <button class="export-btn" onclick="exportSummary()" style="margin-left: 10px;">Export Summary Report</button>
        </div>
    </div>

    <script>
        // Initialize the application
        document.addEventListener('DOMContentLoaded', function() {
            loadData();
            updateAllScores();
        });

        function updateStatus(selectElement) {
            const row = selectElement.closest('tr');
            const scoreCell = row.querySelector('.score-cell');
            const status = selectElement.value;
            
            // Update score based on status
            let score = 0;
            switch(status) {
                case 'leading': score = 3; break;
                case 'working': score = 2; break;
                case 'opportunity': score = 1; break;
                case 'no-opportunity': score = 0; break;
            }
            
            scoreCell.textContent = score;
            
            // Update row styling
            row.classList.remove('status-leading', 'status-working', 'status-opportunity', 'status-no-opportunity');
            if (status !== 'opportunity') {
                row.classList.add(`status-${status}`);
            }
            
            updateAllScores();
            saveData();
        }

        function updateAllScores() {
            const categories = ['impact', 'influence', 'expertise', 'attributes'];
            let totalScore = 0;
            let totalPossible = 0;
            
            categories.forEach(category => {
                const rows = document.querySelectorAll(`tr[data-category="${category}"]`);
                let categoryScore = 0;
                let categoryPossible = 0;
                
                rows.forEach(row => {
                    const score = parseInt(row.querySelector('.score-cell').textContent);
                    categoryScore += score;
                    categoryPossible += 3;
                });
                
                const percentage = Math.round((categoryScore / categoryPossible) * 100);
                document.getElementById(`${category}-score`).textContent = percentage + '%';
                
                totalScore += categoryScore;
                totalPossible += categoryPossible;
            });
            
            const overallPercentage = Math.round((totalScore / totalPossible) * 100);
            document.getElementById('overall-score').textContent = overallPercentage + '%';
        }

        function saveData() {
            const data = {
                requirements: {},
                notes: {
                    actionItems: document.getElementById('action-items').value,
                    discussionPoints: document.getElementById('discussion-points').value,
                    additionalNotes: document.getElementById('additional-notes').value
                }
            };
            
            // Save each requirement row
            document.querySelectorAll('tr[data-category]').forEach((row, index) => {
                const select = row.querySelector('.status-select');
                const evidenceTextarea = row.querySelector('.evidence-textarea:not(.manager-textarea)');
                const managerTextarea = row.querySelector('.manager-textarea');
                
                data.requirements[index] = {
                    status: select.value,
                    evidence: evidenceTextarea.value,
                    managerReflection: managerTextarea.value
                };
            });
            
            // Store in memory
            window.promotionData = data;
        }

        function loadData() {
            if (window.promotionData) {
                const data = window.promotionData;
                
                // Load requirement data
                document.querySelectorAll('tr[data-category]').forEach((row, index) => {
                    if (data.requirements[index]) {
                        const req = data.requirements[index];
                        
                        // Set status
                        const select = row.querySelector('.status-select');
                        select.value = req.status;
                        updateStatus(select);
                        
                        // Set evidence
                        const evidenceTextarea = row.querySelector('.evidence-textarea:not(.manager-textarea)');
                        evidenceTextarea.value = req.evidence || '';
                        
                        // Set manager reflection
                        const managerTextarea = row.querySelector('.manager-textarea');
                        managerTextarea.value = req.managerReflection || '';
                    }
                });
                
                // Load notes
                if (data.notes) {
                    document.getElementById('action-items').value = data.notes.actionItems || '';
                    document.getElementById('discussion-points').value = data.notes.discussionPoints || '';
                    document.getElementById('additional-notes').value = data.notes.additionalNotes || '';
                }
            }
        }

        function exportToCSV() {
            saveData();
            
            let csv = 'Category,Requirement,Status,Score,Employee Evidence,Manager Reflections\n';
            
            document.querySelectorAll('tr[data-category]').forEach(row => {
                const category = row.getAttribute('data-category');
                const title = row.querySelector('.requirement-title').textContent;
                const status = row.querySelector('.status-select').value;
                const score = row.querySelector('.score-cell').textContent;
                const evidence = row.querySelector('.evidence-textarea:not(.manager-textarea)').value.replace(/"/g, '""');
                const managerReflection = row.querySelector('.manager-textarea').value.replace(/"/g, '""');
                
                csv += `"${category}","${title}","${status}","${score}","${evidence}","${managerReflection}"\n`;
            });
            
            // Add notes section
            csv += '\n"Notes Section"\n';
            csv += `"Action Items","${document.getElementById('action-items').value.replace(/"/g, '""')}"\n`;
            csv += `"Discussion Points","${document.getElementById('discussion-points').value.replace(/"/g, '""')}"\n`;
            csv += `"Additional Notes","${document.getElementById('additional-notes').value.replace(/"/g, '""')}"\n`;
            
            const blob = new Blob([csv], { type: 'text/csv' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'senior_professor_promotion_assessment.csv';
            a.click();
            URL.revokeObjectURL(url);
        }

        function exportSummary() {
            saveData();
            
            let summary = "SENIOR INBOUND PROFESSOR PROMOTION ASSESSMENT - SPREADSHEET SUMMARY\n";
            summary += "=" .repeat(75) + "\n\n";
            
            // Overall scores
            summary += "OVERALL READINESS SCORES:\n";
            summary += "-".repeat(25) + "\n";
            summary += `Overall: ${document.getElementById('overall-score').textContent}\n`;
            summary += `Impact: ${document.getElementById('impact-score').textContent}\n`;
            summary += `Influence: ${document.getElementById('influence-score').textContent}\n`;
            summary += `Expertise: ${document.getElementById('expertise-score').textContent}\n`;
            summary += `Core Attributes: ${document.getElementById('attributes-score').textContent}\n\n`;
            
            // Detailed breakdown
            summary += "DETAILED ASSESSMENT:\n";
            summary += "-".repeat(20) + "\n\n";
            
            const categories = ['impact', 'influence', 'expertise', 'attributes'];
            categories.forEach(category => {
                summary += `${category.toUpperCase()} REQUIREMENTS:\n`;
                
                document.querySelectorAll(`tr[data-category="${category}"]`).forEach(row => {
                    const title = row.querySelector('.requirement-title').textContent;
                    const status = row.querySelector('.status-select').value;
                    const score = row.querySelector('.score-cell').textContent;
                    const evidence = row.querySelector('.evidence-textarea:not(.manager-textarea)').value;
                    const managerReflection = row.querySelector('.manager-textarea').value;
                    
                    summary += `\n• ${title}\n`;
                    summary += `  Status: ${status} (Score: ${score})\n`;
                    if (evidence.trim()) {
                        summary += `  Evidence: ${evidence}\n`;
                    }
                    if (managerReflection.trim()) {
                        summary += `  Manager: ${managerReflection}\n`;
                    }
                });
                summary += "\n";
            });
            
            // Notes section
            const actionItems = document.getElementById('action-items').value;
            const discussionPoints = document.getElementById('discussion-points').value;
            const additionalNotes = document.getElementById('additional-notes').value;
            
            if (actionItems.trim() || discussionPoints.trim() || additionalNotes.trim()) {
                summary += "NOTES & ACTION ITEMS:\n";
                summary += "-".repeat(20) + "\n";
                
                if (actionItems.trim()) {
                    summary += "\nAction Items:\n" + actionItems + "\n";
                }
                if (discussionPoints.trim()) {
                    summary += "\nDiscussion Points:\n" + discussionPoints + "\n";
                }
                if (additionalNotes.trim()) {
                    summary += "\nAdditional Notes:\n" + additionalNotes + "\n";
                }
            }
            
            const blob = new Blob([summary], { type: 'text/plain' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'senior_professor_promotion_summary.txt';
            a.click();
            URL.revokeObjectURL(url);
        }
    </script>
</body>
</html>
