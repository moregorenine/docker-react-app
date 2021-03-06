# 간단한 어플을 실제로 배포해보기(개발 환경 부분)
## 1. 리액트 앱 설치하기
### 1.1. react 개발 환경 설치
```sh
npx create-react-app ./
```
## 2. 도커를 이용하여 리액트 앱 실행하기
```docker
docker build -f Dockerfile.dev -t moregorenine/docker-react-app ./
```
- -f : 이미지를 빌드할 때 쓰일 Dockerfile을 임의로 지정해 준다.
## 3. 생성된 도커 이미지로 리액트 앱 실행해보기
```docker
docker run -it -p 3000:3000 moregorenine/docker-react-app
```
## 4. 도커 볼륨을 이용한 소스 코드 변경
```docker
//windows
docker run -it -p 3000:3000 -v /usr/src/app/node_modules -v %cd%:/usr/src/app moregorenine/docker-react-app
or
//mac
docker run -it -p 3000:3000 -v /usr/src/app/node_modules -v $(pwd):/usr/src/app moregorenine/docker-react-app
```
## 5. 도커 컴포즈로 좀 더 간단하게 앱 실행해보기
```docker
docker run -it moregorenine/docker-react-app npm run test
```
## 6. 리액트 앱 테스트 하기
```docker
docker-compose up
```
## 7. 운영환경을 위한 Nginx
## 8. 운영환경 도커 이미지를 위한 Dockerfile 작성하기
```dockerfile
FROM nginx
EXPOSE 80
COPY --from=builder /usr/src/app/build /usr/share/nginx/html
```
```docker
docker run -p 8080:80 moregorenine/docker-react-app
```


# 간단한 어플을 실제로 배포해보기(테스트 & 배포 부분)
# 1. Travis CI 이용 순서
[https://travis-ci.org/](https://travis-ci.org/)
# 4. .travis.yml 파일 작성하기 (테스트까지)
# 5. AWS 알아보기
# 6. Elastic Beanstalk 환경 구성하기
# 7. .travis.yml 파일 작성하기 (배포 부분)
# 8. Travis CI의 AWS접근을 위한 API 생성