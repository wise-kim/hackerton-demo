<script>
  import 'bootstrap/dist/css/bootstrap.min.css';

  import { Image, Navbar, NavbarBrand, Col, Container, Row, Input, Button, Card, CardHeader, CardTitle, CardBody, ListGroup, ListGroupItem } from 'sveltestrap';
  import lang from "./assets/constant"
  let currLang = "언어설정"
  let currKorNewsObj={
    id:'',
    ttle:'',
    content: ''
  }

  let currNews = ""
  let isAudio = false
  const onChange = (target)=>{
    isAudio = false
    currNews = ''
    currLang = target.value
  }

  const onClickNews = (item)=>{
    isAudio = false
    currNews = ''
    currLang = '언어설정'
    if(item.disable){
      currKorNewsObj = {
    id:'',
    ttle:'',
    content: ''
  }
      return
    }
    currKorNewsObj = item
  }

  const onClickTranslate = ()=>{
    switch (currLang){
      case 'NEWS_JP' : 
        if(currKorNewsObj.id == '1'){
          currNews = lang.NEWS_JP;
        }else if(currKorNewsObj.id == '2'){
          currNews = lang.NEWS_JP2;
        }
        break;
      case 'NEWS_ID':
        if(currKorNewsObj.id == '1'){
          currNews = lang.NEWS_ID;
        }else if(currKorNewsObj.id == '2'){
          currNews = lang.NEWS_ID2;
        }
        break;
      // no default
    }
    isAudio = true
  }

  const onPlay = (id)=>{
    let audioEl = document.getElementById(id);
    // audioEl.play();
  }

</script>
<Navbar color="light" light class="mb-4">
  <NavbarBrand href="/">K-NewsWave</NavbarBrand>
  <Image style="width:120px" src="https://wise-kim.github.io/hackerton-demo/img/ihopper-logo.png" alt="아이호퍼"></Image>
</Navbar>

<Container xl>
  <Row>
    <Col sm="2">
      <ListGroup >
        {#each lang.NEWS_LIST as newsItem}
        <ListGroupItem {newsItem} active={currKorNewsObj.id == newsItem.id} on:click={()=>onClickNews(newsItem)}>
          <Row> <Col> <span class="title"> {newsItem.ttle}</span></Col></Row>
          <Row><Col>
              <div class='flex'>
                <span class="font-sm">  {newsItem.com}  </span>
                <span class="font-sm">  {newsItem.journalis}  </span>
              </div> 
            </Col></Row>
          <Row>  <Col><p class="font-sm">  {newsItem.dttm}</p>  </Col></Row>
        </ListGroupItem>
        {/each}
      </ListGroup>
    </Col>
    <Col xs="6" sm="4">
      <Card>
        <CardHeader>
          <CardTitle>한국어 뉴스 기사</CardTitle>
        </CardHeader>
        <CardBody>
          <Input class="text-box" type="textarea" name="text" id="" value={currKorNewsObj.content} disabled/>
        </CardBody>
      </Card>
    </Col>
    <Col xs="6" sm="4">
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
  {#if isAudio && currLang == 'NEWS_ID' && currKorNewsObj.id == '1'}
  <Row>
    <Col xl="10" class="mt-4">
      <audio controls id="audioID">
        <source src="https://wise-kim.github.io/hackerton-demo/audio/NEWS_ID.mp3" type="audio/mpeg">
      </audio>
      <!-- <div id="audioplayer" on:click={onPlay('audioID')}>
        <span id="pButton" >▶</span>
        <div id="timeline">
          <div id="playhead"></div>
        </div>
      </div> -->
    </Col>
  </Row>
  {/if}
  {#if isAudio && currLang == 'NEWS_ID' && currKorNewsObj.id == '2'}
  <Row>
    <Col xl="10" class="mt-4">
      <audio controls id="audioID">
        <source src="https://wise-kim.github.io/hackerton-demo/audio/NEWS_ID2.mp3" type="audio/mpeg">
      </audio>
      <!-- <div id="audioplayer" on:click={onPlay('audioID')}>
        <span id="pButton" >▶</span>
        <div id="timeline">
          <div id="playhead"></div>
        </div>
      </div> -->
    </Col>
  </Row>
  {/if}
  {#if isAudio && currLang == 'NEWS_JP' && currKorNewsObj.id == '1'}
  <Row>
    <Col class="mt-4">
      <audio controls id="audioJP">
        <source src="https://wise-kim.github.io/hackerton-demo/audio/NEWS_JP.mp3" type="audio/mpeg">
      </audio>
    </Col>
  </Row>
  {/if}
  {#if isAudio && currLang == 'NEWS_JP' && currKorNewsObj.id == '2'}
  <Row>
    <Col class="mt-4">
      <audio controls id="audioJP">
        <source src="https://wise-kim.github.io/hackerton-demo/audio/NEWS_JP2.mp3" type="audio/mpeg">
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
  .flex{
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .title{
    font-weight: bold;
  }
  .font-sm{
    font-size: 14px;
  }
  #pButton {
  float: left;
}

#audioplayer{
  display: flex;
  align-items: center;
}
#timeline {
  width: 90%;
  height: 2px;
  margin-top: 20px;
  margin-left: 10px;
  float: left;
  -webkit-border-radius: 15px;
  border-radius: 15px;
  background: rgba(0, 0, 0, 0.3);
}

#pButton {
  margin-top: 12px;
  cursor: pointer;
}

#playhead {
  width: 8px;
  height: 8px;
  -webkit-border-radius: 50%;
  border-radius: 50%;
  margin-top: -3px;
  background: black;
}

</style>
