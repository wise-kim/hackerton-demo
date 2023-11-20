<script>
  import 'bootstrap/dist/css/bootstrap.min.css';

  import { Image, Navbar, NavbarBrand, Col, Container, Row, Input, Button, Card, CardHeader, CardTitle, CardBody } from 'sveltestrap';
  import lang from "./assets/constant"
  let currLang = "언어설정"
  let currNews = ""
  let isAudio = false
  const onChange = (target)=>{
    isAudio = false
    currLang = target.value
  }

  const onClickTranslate = ()=>{
    switch (currLang){
      case 'NEWS_JP' : 
        currNews = lang.NEWS_JP;
        break;
      case 'NEWS_ID':
        currNews = lang.NEWS_ID;
        break;
      // no default
    }
    isAudio = true

  }
</script>
<Navbar color="light" light class="mb-4">
  <NavbarBrand href="/">K-NewsWave</NavbarBrand>
  <Image style="width:120px" src="/img/ihopper-logo.png" alt="아이호퍼"></Image>
</Navbar>

<Container lg>
  <Row>
    <Col xs="6" sm="5">
      <Card>
        <CardHeader>
          <CardTitle>한국어 뉴스 기사</CardTitle>
        </CardHeader>
        <CardBody>
          <Input class="text-box" type="textarea" name="text" id="" value={lang.NEWS_KR} disabled/>
        </CardBody>
      </Card>
    </Col>
    <Col xs="6" sm="5">
      <Card >
        <CardHeader>
          <CardTitle>번역 뉴스 기사</CardTitle>
        </CardHeader>
        <CardBody>
          <Input  class="text-box" type="textarea" name="text" id="" value={currNews} disabled/>
        </CardBody>
      </Card>
    </Col>
    <Col sm="2">
      <Input class="mb-4" type="select" name="select" id="exampleSelect" value={currLang} on:change={(e)=>onChange(e.target)}>
        <option value="언어설정">언어설정</option>
        <option disabled>한국어</option>
        <option value="NEWS_JP">일본어</option>
        <option value="NEWS_ID">인도네시아어</option>
        <option disabled>터키어</option>
        <option disabled>아랍어</option>
      </Input>
      <Button  class="mt-4" on:click={onClickTranslate}>오디오 뉴스 생성</Button>
    </Col>
  </Row>
  {#if isAudio && currLang == 'NEWS_ID'}
  <Row>
    <Col  class="mt-4">
      <audio controls >
        <source src="/audio/NEWS_ID.mp3" type="audio/mpeg">
      </audio>
    </Col>
  </Row>
  {/if}
  {#if isAudio && currLang == 'NEWS_JP'}
  <Row>
    <Col  class="mt-4">
      <audio controls >
        <source src="/audio/NEWS_JP.mp3" type="audio/mpeg">
      </audio>
    </Col>
  </Row>
  {/if}
</Container>


<style>
  :global(.text-box){
    height: 54vh;
    resize: none;
  }

</style>
