prod - ssh [rails@158.160.130.172](mailto:rails@158.160.130.172)  
stage - ssh rails@158.160.130.137  
  
cd ~/dcrt-hrm-front/huntlee-frontend

git pull && rm -rf .nuxt && rm -rf .output && rm -rf node_modules && bun install && bun run build && pm2 restart huntlee

  
  
rm -rf .nuxt && rm -rf .output && bun run dev

rm -rf .nuxt && rm -rf .output && rm -rf node_modules && bun install && bun run build && node .output/server/index.mjs

  
  
insomnia  
JKL36jA!E@sRfTF  
  
stage

gitlab-runner register

  --url https://gitlab.violinorg.ru

  --token glrt-A4YoaMRDzLB26f_s7Lsp

  

  

[http://localhost:3000/main/applicants?status_from=2024-09-01&status_to=2024-09-02&account_source_id=2479&tags[]=164&tags[]=151&skill_ids[]=47&skill_ids[]=909&skill_ids[]=1&country_id=172&position=React+Frontend+Developer(JavaScript,+TypeScript,+React)&company=NeuroCity&total_experience=1&age_from=1&age_to=2&salary_from=1&salary_to=2&currency=RUB&employments[]=1&employments[]=2&employments[]=3&admin_user_id=49&vacancy_id=1804&status_id=2464&email=asdasd@dasd.asd&phone=12312312&tg=asdsad&only_mine=true&page=1&per_page=20](http://localhost:3000/main/applicants?status_from=2024-09-01&status_to=2024-09-02&account_source_id=2479&tags%5B%5D=164&tags%5B%5D=151&skill_ids%5B%5D=47&skill_ids%5B%5D=909&skill_ids%5B%5D=1&country_id=172&position=React+Frontend+Developer(JavaScript,+TypeScript,+React)&company=NeuroCity&total_experience=1&age_from=1&age_to=2&salary_from=1&salary_to=2&currency=RUB&employments%5B%5D=1&employments%5B%5D=2&employments%5B%5D=3&admin_user_id=49&vacancy_id=1804&status_id=2464&email=asdasd@dasd.asd&phone=12312312&tg=asdsad&only_mine=true&page=1&per_page=20)

  

  

docker run -e MODE=development -e APP_PROTOCOL="https" -e APP_DOMAIN="stage.huntlee.ru" -e APP_HEAD_META_CONTENT="Название" -e APP_HEAD_TITLE="Название" -e APP_SWAGGER_SCHEMA_YAML_URL="https://stage.huntlee.ru/api-docs/v1/swagger.yaml" -p 3000:3000 -p 3001:3001 nexus.violinorg.ru:19133/frontend/huntlee-frontend:1.0.0-979.dc629182