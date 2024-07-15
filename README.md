# Evangelical_College_Finder
Making a list of best valued US Colleges and Universities for WORLDWIDE highschool student who wanted to go to US for Bachelor degree. And researches on how to use Chat-GPT to generate web crawler program that can be used by ANYONE. (Still in process...)
            
    import requests
    from bs4 import BeautifulSoup
    
    url = "http://www.qianmu.org/2023USNEWS%E7%BE%8E%E5%9B%BD%E6%9C%BA%E6%A2%B0%E5%B7%A5%E7%A8%8B%E6%8E%92%E5%90%8D"
    
    response = requests.get(url)
    
    if response.status_code == 200:
        
        soup = BeautifulSoup(response.content, 'html.parser')
        
       
        rankings_table = soup.find('table')  # Assuming the data is in a table
    
        
        data = []
        for row in rankings_table.find_all('tr'):
            cells = row.find_all('td')
            row_data = [cell.get_text(strip=True) for cell in cells]
            data.append(row_data)
    
        for row in data:
            print(row)
    else:
        print("Failed to retrieve the webpage. Status code:", response.status_code)
              
hi 
    
    import requests
    from bs4 import BeautifulSoup
    import pandas as pd

    url = "http://www.qianmu.org/2023USNEWS%E7%BE%8E%E5%9B%BD%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%B7%A5%E7%A8%8B%E6%8E%92%E5%90%8D"

    response = requests.get(url)

    if response.status_code == 200:
    
        soup = BeautifulSoup(response.text, 'html.parser')
    
    
        content = soup.find(class_='col-md-12')
    
        if content:
        
            table = content.find('table')
        
            if table:
            
                rows = []
                for tr in table.find_all('tr')[1:]:  
                    cells = tr.find_all('td')
                    if len(cells) >= 2:
                        rank = cells[0].text.strip()
                        school_name = cells[1].text.strip()
                        rows.append([rank, school_name])
            
            
                df = pd.DataFrame(rows, columns=["Rank", "School Name"])
            
            
                df.to_excel('1_computer_engineering2_ranking.xlsx', index=False)
            
                print("数据已成功写入 Excel 文件")
            else:
                print("未找到表格")
        else:
            print("未找到 class 为 'col-md-12' 的内容")
    else:
        print("无法获取网页内容，状态码:", response.status_code)
